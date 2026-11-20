# TVET RBM&E Workshop Studio — GitHub Pages edition

A static, local-first reconstruction of the uploaded XAMPP application. Deploy this folder to GitHub Pages. The application stores workshop records in the browser's **IndexedDB**, caches its application shell with a service worker, and supports JSON backup/restore and CSV exports.

## Important deployment and identity limitations

GitHub Pages serves static files only. It does not run the original PHP, MySQL/MariaDB, PHP sessions, prepared statements, or server-side authorization. This edition therefore replaces those services with browser-local storage.

- **Data is per browser profile and website origin.** A participant's phone and laptop do not share records automatically. A different browser, private window, cleared site data, or a different Pages URL is a separate data store.
- **There is no secure shared multi-user authentication.** The local profile and role selector are workflow conveniences, not a security boundary. Anyone with browser access can inspect or modify local data. Do not use this edition for sensitive personal information or confidential institutional records.
- **Facilitator/admin roles are local UI permissions only.** They cannot enforce access control against a technically capable user.
- **Offline support:** after the first successful visit, the service worker caches the app shell. IndexedDB data remains available on that device while the browser retains site data.
- For real group collaboration, cross-device synchronization, secure accounts, audit trails, and enforceable permissions, deploy the original PHP application on a PHP/MySQL host or add a backend (for example Supabase/Firebase) with proper row-level authorization. GitHub Pages alone cannot provide these features.

## Deploy to GitHub Pages

1. Create a GitHub repository (for example `tvet-rbme-workshop`).
2. Upload the contents of this folder to the repository root (so `index.html` is at the root).
3. Open **Settings → Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**, choose `main` and `/ (root)`, then Save.
5. Open the published Pages URL over HTTPS. The browser creates its local database on first launch.

No build step, PHP runtime, SQL import, or environment variables are required.

## First sign-in

The first launch creates a demonstration workspace with:

- Local administrator profile: `admin@local.test`
- Passphrase: `admin123`
- Sample workshop, institution, welding initiative, results components and one sample indicator.

Sign in and change the local passphrase from **Local data & settings**. Add participant profiles under **Users**. The demo login is not a secure account and must not be reused as a real password.

## Functional areas

| Original application area | Static edition |
|---|---|
| Six guided learning pathways | Six pathway workspaces with CRUD forms |
| Initiative / pre-program assessment | Initiative records |
| Results framework | Impact-to-input components, assumptions and risks |
| Indicator registry | SMART indicator fields, baseline/target date validation |
| RBM&E plan | Overview, monitoring matrix, evaluation questions, tools, reports and feedback |
| Performance dashboard | Performance records and progress-to-target calculation |
| Institutional action plan | Gap scoring (severity × urgency) and action records |
| Re-entry commitment | Individual commitment records |
| Institutions, workshops, users, groups and group members | Local CRUD records |
| Output portfolio | Printable pathway data portfolio |
| Export | Complete JSON backup/restore and per-table CSV |
| XAMPP deployment | GitHub Pages static deployment |

## Data safety

Use **Reports & exports → Export complete JSON backup** frequently. Keep the downloaded file somewhere outside the browser. Restore replaces the current local dataset. The app cannot recover data after browser site data is erased unless you have a backup.

## Verification performed on this reconstruction

- JavaScript syntax checked with Node.js.
- ZIP CRC integrity checked against the uploaded archive.
- PHP source files in the uploaded archive passed `php -l` syntax checks.
- Static source inspection found that the uploaded package references `install.php` in its README and router, but `install.php` is absent from the archive. The README also references `config.local.php`, not included in the archive.
- No live PHP/MySQL integration, cross-browser, mobile device, penetration, concurrency, or GitHub Pages hosted-browser acceptance test is claimed here.

## Source lineage

This reconstruction was based on the uploaded `TVET_RBME_Workshop.zip`, including its six pathway definitions, entity catalogue, database schema, facilitator guide and README. It is a browser-local implementation, not a drop-in execution of the original PHP backend. Review `docs/MIGRATION_NOTES.md` before using it in a real workshop.
