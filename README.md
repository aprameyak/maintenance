# Maintenance

A tech debt log for people who look after several repositories. Record outdated dependencies, known vulnerabilities, and estimated fix effort for each repo, then view them sorted by risk.

## Features

- Add a repo with its language, outdated dependency count, vulnerability count, and estimated hours to fix
- Repos are listed in order of vulnerability count, highest first
- A summary endpoint totals repos, vulnerabilities, and effort hours
- Entries are saved to a local JSON file

## Getting started

Requires Node.js.

```bash
npm install
npm start
```

Then open http://localhost:3010. `npm run dev` runs the same command.

## How it works

- `index.html` contains the "Add Repository" form and the repo list. It calls the API at `http://localhost:3010`.
- `server.js` is an Express app that serves the page and exposes:
  - `POST /api/repos` to save a repo entry.
  - `GET /api/repos` to list repos sorted by vulnerabilities.
  - `GET /api/debt` to return totals across all repos.
- Data is written to `data.json`, created on first run and ignored by git.
- `utils.js` holds validation and file helpers that are not yet wired into `server.js`.

## Status

Prototype. Counts are entered by hand; nothing scans real dependencies. The two GET handlers currently reference an undefined `res` variable, so listing repos and the summary fail until that is fixed in `server.js`.

## License

MIT, see [LICENSE](LICENSE).
