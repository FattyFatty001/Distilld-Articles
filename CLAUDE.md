# ⛔ STOP — READ THIS FIRST

## 🚨 MANDATORY: `git pull` BEFORE touching ANY file

**This directory is a git clone of the production article CDN.** The production server (`deliver.py`) writes article JSON files directly to the GitHub repo via the GitHub Contents API. This means **the local copy on this machine can be stale at any moment** — the server may have published new articles, rebuilt indexes, or updated the manifest since the last pull.

### BEFORE you read or edit ANY file in this directory:
```sh
cd "Distilld Articles" && git pull
```

### Why this matters:
- Reading a stale file means you're working with outdated article data, source indexes, or manifest metadata.
- Editing a stale file means you'll get a merge conflict — or worse, silently clobber a change the server published.
- The server doesn't use this local clone at all. The only way this clone stays current is `git pull`.

### Workflow for any file operation in this directory:
1. **`git pull`** — always first
2. **Read or edit** the file(s)
3. **If you edited**: `git add`, `git commit`, `git push`

### What lives here:
```
articles/
├── manifest.json                    — Source list + timestamps + index_path per source
├── Index/{province}/                — Per-source article indexes
└── YYYY/MM/DD/{id}_{src}_{slug}.json — Individual article briefs
```

**Role**: Single source of truth for article content, consumed by the Legal Alert App via raw.githubusercontent.com.

**Test counterpart**: `FattyFatty001/Distilld-Articles-TEST` — used by the test server instance. The test server publishes test articles to this repo via the GitHub Contents API and the local `Distilld Articles Test/` directory is a git clone of this test repo. Treat it with the same git-pull-before-reading discipline as the production repo.
