# Voter Search

In-browser SQLite voter search. No backend. Works on phones.

## Deploy to Vercel

This is a static site. Just deploy the folder as-is.

- `index.html` and `voters.db.gz` must sit in the SAME folder.
- For a plain static site, keep them both in the root (already done).
- If your setup serves static assets from `public/`, a copy of `voters.db.gz`
  is also in `public/`. Move `index.html` wherever your framework expects,
  and make sure the path in `index.html` (`DB_URL = "voters.db.gz"`) still
  points to where the file is served.

### Quick deploy
1. Upload this folder to a new Vercel project (or `vercel` CLI in this folder).
2. Done.

## How it works
- First visit downloads `voters.db.gz` (~12MB), decompresses it in the browser,
  caches the result in IndexedDB.
- Later visits load from cache instantly, offline.
- Search runs against in-browser SQLite (~80ms), all 353k rows.

## Data
- 353,216 voter rows, columns: AC, part_no, sl_no, door_no, voter_name,
  relation, relation_name, gender, age, epic_id.
- Search covers voter_name (Telugu), epic_id, relation_name, door_no.
  Pure digits also match part_no exactly.
