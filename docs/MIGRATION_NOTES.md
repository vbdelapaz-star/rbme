# Migration and integrity notes

## Uploaded package inventory

The ZIP contains 30 entries and the following application layers:

- PHP router and application logic: `index.php`, `app/core.php`, `modules.php`, `entities.php`, `calc.php`, `crud.php`, `outputs.php`, `pages.php`, `seed.php`.
- MySQL schema: `database/schema.sql` (24 table definitions).
- Browser assets: `assets/app.js`, `assets/style.css`.
- Documentation and an end-to-end Python test script.

## Findings from static inspection

1. `README.md` instructs the operator to open `/install.php`, and `index.php` redirects to `install.php` when `app/installed.lock` is absent. **No `install.php` exists in the supplied archive.** A fresh deployment following the supplied instructions therefore cannot complete installation as documented.
2. `config.php` says the installer writes `config.local.php`, but no installer or local override file is present in the ZIP.
3. `app/installed.lock` is included in the archive. This makes the router bypass its installer redirect, but it does not provision a database or administrator account.
4. All supplied PHP files passed PHP syntax lint (`php -l`) in this review. This is syntax-only; it does not prove runtime correctness.
5. The README reports a 147-check PHP/MariaDB E2E run, but that result is a statement in the source README. It was not independently reproduced in this review.
6. The supplied E2E test requires a running PHP/MySQL environment and was not run against a live database here.

## Migration decisions

- Preserved the six learning pathways and their expected outputs as described in `app/modules.php` and the supplied README.
- Recreated the principal entity areas from `app/entities.php`: institutions, workshops, users, work groups, group members, initiatives, results-chain components, indicators, plan records, performance records, decisions, gaps, actions, re-entry commitments, feedback and evaluations.
- Replaced PHP/MySQL persistence with IndexedDB and a JSON import/export format.
- Added a service-worker cache for the static application shell.
- Added printable portfolio output, CSV export and local record management.
- Retained a demonstration workshop and welding case as seed data.

## Known gaps versus the XAMPP system

The static edition cannot provide the original server-side security controls, shared multi-user editing, account provisioning across devices, PHP session management, CSRF protection, server-side IDOR prevention, authoritative audit log, database constraints/cascade rules, or the original submit/review queue. Local role-based UI is not security enforcement. The current output portfolio is a printable data compilation, not a server-generated DOC/Word export. Program evaluation and peer feedback records are maintained locally, but there is no remote facilitator review workflow.

These are architectural constraints, not bugs that can be fixed by adding a GitHub Pages setting. For a production workshop with multiple participants collaborating from separate devices, use a backend-enabled deployment.
