---
scope: 'The Warracker web app and its Flask API: accounts and sign-in, warranties, documents, claims, tags, the status dashboard, expiry notifications and administration.'
method: Static inspection of the pinned source, migrations and README; nothing was run.
covered:
- description: API routes for accounts, warranties, claims, tags, documents, statistics and administration.
  paths:
  - backend/auth_routes.py
  - backend/warranties_routes.py
  - backend/tags_routes.py
  - backend/file_routes.py
  - backend/statistics_routes.py
  - backend/admin_routes.py
  - backend/auth_utils.py
- description: Single sign-on, notification scheduling, Apprise, Paperless-ngx, audit logging and shared helpers.
  paths:
  - backend/oidc_handler.py
  - backend/notifications.py
  - backend/apprise_handler.py
  - backend/paperless_handler.py
  - backend/audit_logger.py
  - backend/utils.py
  - backend/db_handler.py
  - backend/__init__.py
  - backend/config.py
- description: Database migrations defining what is kept.
  paths:
  - backend/migrations/
- description: Web pages and their scripts for sign-in, registration, password reset, Home, the status dashboard and settings.
  paths:
  - frontend/index.html
  - frontend/login.html
  - frontend/register.html
  - frontend/reset-password.html
  - frontend/reset-password-request.html
  - frontend/status.html
  - frontend/status.js
  - frontend/settings-new.html
  - frontend/settings-new.js
  - frontend/js/
  - frontend/script.js
  - frontend/auth.js
  - frontend/auth-redirect.js
  - frontend/auth-redirect.html
  - frontend/registration-status.js
  - frontend/file-utils.js
exclusions:
- description: Container, web server, process supervision and release plumbing.
  paths:
  - Dockerfile
  - Docker/
  - docker-compose.yml
  - nginx.conf
  - backend/gunicorn_config.py
  - backend/fix_permissions.py
  - backend/fix_permissions.sql
  - backend/extensions.py
  - unraid/
  - .github/
  - renovate.json
- description: Translation catalogs, styles, vendored libraries, icons and images.
  paths:
  - locales/
  - backend/localization.py
  - backend/messages.pot
  - babel.cfg
  - frontend/vendor/
  - frontend/js/lib/i18next.min.js
  - frontend/img/
  - frontend/style.css
  - frontend/settings-styles.css
  - frontend/header-fix.css
  - frontend/mobile-header.css
  - images/
- description: Page chrome, theme, service worker and browser-side layout fixes.
  paths:
  - frontend/footer-content.js
  - frontend/footer-fix.js
  - frontend/fix-auth-buttons.js
  - frontend/fix-auth-buttons-loader.js
  - frontend/include-auth-new.js
  - frontend/mobile-menu.js
  - frontend/theme-loader.js
  - frontend/sw.js
  - frontend/manifest.json
  - frontend/chart.js
  - frontend/auth-new.js
- description: 'Admin diagnostics and maintenance: scheduler status, Apprise URL validation, supported services, custom Apprise messages, configuration reload, Paperless-ngx connection tests and invalid-reference cleanup.'
  paths:
  - frontend/settings-new.js
  - backend/apprise_handler.py
  - backend/file_routes.py
- description: The about page and its release check against GitHub, peripheral to keeping warranties.
  paths:
  - frontend/about.html
  - frontend/version-checker.js
unmapped:
- description: Paperless-ngx document browsing, search and linking by title, left to Paperless-ngx, which owns those documents.
  paths:
  - frontend/js/components/paperless.js
- description: 'The hand-off from registration to adding a first warranty is not a Journey: the person signs in partway, which pdd-kit 0.37.0 cannot join.'
  paths:
  - frontend/register.html
limitations:
- description: Which of the two Home scripts handles a control when both define it could not be settled without running the page.
  paths:
  - frontend/script.js
- description: The admin-only all-warranties endpoint and the warranty debug endpoint have no caller in the web app.
  paths:
  - backend/warranties_routes.py
---

# Coverage
