# MAYUU CONTROL CENTRE

A dark, responsive repository command-centre UI starter for the `mayuu-p` GitHub workspace.

## Current state

- Windows-inspired visual lock screen and dashboard shell.
- Overview metrics and searchable repository cards.
- Responsive navigation for desktop and mobile.
- Frontend expects a same-origin backend endpoint: `GET /api/github/repos`.
- GitHub write actions are deliberately not exposed until the backend has authorization, CSRF protection, permission checks and audit logging.

## Important security note

The lock screen in this starter is **visual only**. It is not authentication and does not protect static files. Do not deploy sensitive repository data or credentials with this frontend alone. Do not put GitHub tokens, app private keys, or client secrets in browser JavaScript, HTML, or GitHub Pages.

## Production architecture

1. Register a GitHub App owned by the account and install it for all repositories (or explicitly selected repositories).
2. Use a server-side OAuth/web authentication flow and secure, HttpOnly, Secure, SameSite cookies.
3. Keep GitHub App private key and installation token handling exclusively on the server. Mint short-lived installation tokens as needed.
4. Implement `GET /api/github/repos` using the installation token, with pagination.
5. Add webhook handling for repository events and a scheduled reconciliation sync so newly created repositories are discovered.
6. Add server-side endpoints for file CRUD, GitHub Pages settings, workflow dispatch, deployment status and repository settings. Enforce least privilege and explicit confirmation for destructive actions.
7. Store an audit record for every write operation. Add rate limiting, CSRF protection, input validation, secret rotation and backups.

## Local preview

Open `index.html` in a browser. The UI shell works without a backend; repository sync will show a backend-not-connected message until the API is implemented.

## Deployment

A static GitHub Pages deployment can host only the frontend. A separate HTTPS backend is required for secure GitHub integration and password authentication.
