# Messenger Group Control — Railway

## Included features
- Password-protected Flask dashboard
- CSRF protection for POST forms
- Persistent SQLite settings, auto-reply rules, and activity logs
- Command panel for status/logs and enabling/disabling reply configuration
- Group-name and nickname request forms (request logging only)
- Dark/light theme preference
- Cookie JSON syntax/shape validator (does not save or use submitted cookie values)
- Health endpoint at `/health`

## Deploy
1. Upload `app.py`, `requirements.txt`, `Procfile`, and `README.md` to a GitHub repository root.
2. In Railway, create a project from the repository.
3. Add service variables:
   - `SECRET_KEY`: long random secret (do not share)
   - `ADMIN_PASSWORD`: strong unique dashboard password
   - `DB_PATH`: `/data/dashboard.db`
   - `COOKIE_SECURE`: `1` for the Railway HTTPS domain (default)
4. Add a Railway Volume mounted at `/data` for persistent database storage.
5. Deploy and open the Railway-generated domain.
6. Sign in using `ADMIN_PASSWORD`.

If testing on plain local HTTP, set `COOKIE_SECURE=0` locally only. Do not use that setting for a public HTTPS deployment.

## Important capability boundary
This dashboard stores configuration and logs; it does not connect to personal Messenger group chats or execute group renames/nickname changes. Meta's official Messenger Platform is designed for supported Page messaging and does not expose a general-purpose API for arbitrary personal group chats, group names, or member nicknames. Auto-reply rules here are configuration only, not live message automation.

The JSON validator parses the submitted JSON transiently and checks its shape. It does not persist, echo, or use cookie/session values. Do not paste real session cookies into a hosted service.

Before public production use, consider rate limiting, account recovery procedures, and a security review. Never commit secrets to GitHub.
