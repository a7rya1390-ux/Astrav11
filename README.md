# Astrav11
The website of Astra Brand.
<div align="center">
  <img src="static/image/astra-logo.jpg" alt="ASTRA logo" width="180" />
  <h1>ASTRA v11</h1>
  <p><strong>One ecosystem. A world of ideas, creativity, and connection.</strong></p>
  <p>
    An AI-focused web platform bringing together community, technology news,
    achievements, events, digital media, and interactive experiences.
  </p>
</div>---

Contents

- "About Astra" (#about-astra)
- "Platform features" (#platform-features)
- "Technology stack" (#technology-stack)
- "Project structure" (#project-structure)
- "Getting started" (#getting-started)
- "Environment configuration" (#environment-configuration)
- "Django Admin" (#django-admin)
- "Database and safe upgrades" (#database-and-safe-upgrades)
- "Deployment notes" (#deployment-notes)
- "SEO and discoverability" (#seo-and-discoverability)
- "Security and privacy" (#security-and-privacy)
- "License" (#license)
- "Validation status" (#validation-status)
- "Roadmap" (#roadmap)
- "Connect" (#connect)

About Astra

ASTRA is a modular web platform designed to bring several digital experiences into one connected environment. Astra combines an AI assistant, a member community, technology-focused publishing, achievement tracking, seasonal celebrations, and media sections under one visual identity.

Astra v11 builds on the Django application structure and adds expanded member, social, messaging, News, AI, administration, and content-management workflows. It is intended to be maintainable: the main Django project connects separate apps, while uploaded media and the database can be stored independently from deployable source code.

Platform features

Section| What it does
Home| Introduces Astra and highlights featured content through configurable home slides.
About Astra| Explains the platform's mission, vision, values, history, and direction.
Member profiles| Public member pages with posts, follower/following counts, Rank activity, and Awards history.
Astragram| Community feed with image posts, likes, comments, and links to each author's public profile.
Direct Messages| Member-to-member conversations, inbox search, unread state, and message polling.
Astra News| Technology and AI articles, article search, recent hashtag trends, and popular stories based on recorded page views.
Astra AI| Assistant interface with saved conversations for signed-in members; can use built-in knowledge mode or a configured compatible AI provider.
Astra Rank| Achievement submissions with proof images, manual administrator review, points, and leaderboard history.
Astra Awards| Activity-based competition with daily, weekly, monthly, quarterly, and yearly award periods.
Astra Events| Configurable celebrations with scheduled messages, themes, and up to three visual effects per event.
Gallery & Music| Curated image and music sections managed through Django Admin.
Mini Games| A separate lightweight games section.
Help Center & Support| Platform guidance, frequently asked questions, and contact/feedback forms.
Astra Clock| A dedicated clock and date experience.

Rank and Awards are different

- Astra Rank recognises submitted achievements. A submission remains pending until an administrator reviews its proof. Approved categories award the configured Rank points.
- Astra Awards records community activity and period winners. Its scoring is separate from Rank; approved Rank achievements can also contribute to Awards activity totals as configured in the application.
- Winning an Awards period creates an award record; winning does not itself add bonus competition points. Tied highest scorers can each be recorded as winners.

Current Rank point categories

Achievement type| Points
Certificate| 10
Medal| 50
Statistics / graph screenshot| 5
Course completion| 15
Competition award| 30
Community contribution| 20

These values are defined in "rank/models.py". An administrator must approve a proof submission before it contributes to Rank.

Technology stack

- Backend: Python and Django
- Authentication: Django authentication and django-allauth (Google/GitHub providers are optional)
- Database: SQLite by default, with a configurable persistent database path
- Frontend: Django Templates, HTML, CSS, and JavaScript
- Image handling: Pillow
- Static and uploaded files: Django staticfiles and media storage

Declared dependencies are listed in ""requirements.txt"" (requirements.txt): Django ">=5.0,<6.1", django-allauth ">=65.0", and Pillow ">=10.0".

Project structure

astra_v11/
├── accour/       # Accounts, authentication, profiles, follows, legal consent
├── astragram/    # Social feed, posts, comments, likes, direct messages
├── newsroom/    # Articles, News search, topics, view counts
├── rank/         # Achievement submissions, points, leaderboard, Rank prizes
├── awards/       # Activity scoring, competition periods, award records
├── events/       # Scheduled celebrations and visual-effect library
├── core/         # Home, About, Astra AI, Support, shared content and utilities
├── gallery/      # Gallery content
├── music/        # Music content and categories
├── minigames/    # Mini Games section
├── config/       # Django settings, URL routing, sitemap configuration
├── templates/    # Shared templates and Django Admin customisations
├── static/       # CSS, JavaScript, and project assets
├── manage.py
└── requirements.txt

Getting started

1. Requirements

- Python 3.10 or newer
- pip
- A terminal or command prompt

2. Get the project

Clone your GitHub repository or download the source archive, then open a terminal in the folder containing "manage.py".

git clone YOUR_REPOSITORY_URL
cd YOUR_REPOSITORY_FOLDER

Replace the two placeholders with your actual GitHub repository URL and folder name.

3. Create a virtual environment

macOS / Linux / PythonAnywhere Bash:

python3 -m venv .venv
source .venv/bin/activate

Windows PowerShell:

py -m venv .venv
.\.venv\Scripts\Activate.ps1

4. Install dependencies

python -m pip install --upgrade pip
pip install -r requirements.txt

5. Configure local settings

Astra reads configuration from environment variables. The project does not automatically load a ".env" file, so set variables in your shell or hosting platform.

macOS / Linux / PythonAnywhere Bash:

export DJANGO_DEBUG=True
export DJANGO_SECRET_KEY="replace-with-a-long-random-secret"
export DJANGO_ALLOWED_HOSTS="127.0.0.1,localhost"
export DJANGO_TIME_ZONE="UTC"

Generate a suitable development secret with:

python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"

Windows PowerShell:

$env:DJANGO_DEBUG = "True"
$env:DJANGO_SECRET_KEY = "replace-with-a-long-random-secret"
$env:DJANGO_ALLOWED_HOSTS = "127.0.0.1,localhost"
$env:DJANGO_TIME_ZONE = "UTC"

6. Apply database migrations

python manage.py migrate

7. Create an administrator account

python manage.py createsuperuser

Follow the prompts. Keep the password private and do not add credentials to GitHub.

8. Run the development server

python manage.py runserver

Open these local addresses:

- Website: "http://127.0.0.1:8000/"
- Django Admin: "http://127.0.0.1:8000/admin/"

9. Run project checks

python manage.py check
python manage.py test

Environment configuration

All values below are optional unless marked as required for the selected deployment or feature. Set them in the hosting platform's environment-variable panel or shell. Never commit real secrets.

Variable| Purpose| Default / example
"DJANGO_SECRET_KEY"| Django signing secret. Required when "DJANGO_DEBUG=False".| Generate a private random value.
"DJANGO_DEBUG"| Enables or disables debug mode.| "True" locally; "False" in production.
"DJANGO_ALLOWED_HOSTS"| Comma-separated allowed hostnames.| "127.0.0.1,localhost"
"DJANGO_TIME_ZONE"| Django time zone.| "UTC" (for example, "Asia/Tehran")
"DJANGO_DB_PATH"| Absolute path to the persistent SQLite database file.| Defaults to "db.sqlite3" in the project directory.
"DJANGO_MEDIA_ROOT"| Persistent directory for uploaded media.| Defaults to "media/" in the project directory.
"DJANGO_MEDIA_URL"| Public URL prefix for uploaded media.| "/media/"
"DJANGO_SECURE"| Enables HTTPS-related cookie and redirect settings.| "False"; use "True" behind correctly configured HTTPS.
"DJANGO_HTTP_PROTOCOL"| Protocol used for social-auth callback URLs.| "http" locally; "https" in production.
"GOOGLE_OAUTH_CLIENT_ID" / "GOOGLE_OAUTH_CLIENT_SECRET"| Optional Google sign-in credentials.| Not configured.
"GITHUB_OAUTH_CLIENT_ID" / "GITHUB_OAUTH_CLIENT_SECRET"| Optional GitHub sign-in credentials.| Not configured.
"ASTRA_AI_API_KEY"| Optional server-side key for a compatible AI provider.| Empty; built-in knowledge mode is used.
"ASTRA_AI_BASE_URL"| Compatible Chat Completions API base URL.| "https://api.openai.com/v1"
"ASTRA_AI_MODEL"| Model identifier sent to the configured provider.| "gpt-4o-mini"
"ASTRA_AI_TIMEOUT"| Provider request timeout in seconds.| "25"
"DJANGO_EMAIL_BACKEND"| Set to "smtp" to send support emails through SMTP.| Console backend
"EMAIL_HOST", "EMAIL_PORT", "EMAIL_HOST_USER", "EMAIL_HOST_PASSWORD"| SMTP server credentials and port.| Host defaults to "smtp.gmail.com"; port "587".
"CONTACT_EMAIL"| Destination for contact/support email.| Set your preferred project contact address.
"GOOGLE_SITE_VERIFICATION"| Google Search Console HTML verification token.| Empty
"BING_SITE_VERIFICATION"| Bing Webmaster verification token.| Empty
"ALLOW_OAI_SEARCHBOT"| Controls the OAI-SearchBot rule in "robots.txt".| "True"
"ALLOW_GPTBOT"| Controls the GPTBot rule independently.| "False"
"ASTRA_TERMS_VERSION" / "ASTRA_PRIVACY_VERSION"| Versions recorded when members accept the site policies.| Version dates configured in settings.

Optional live AI provider

Astra AI can use a compatible Chat Completions endpoint when "ASTRA_AI_API_KEY" is configured. The API key must remain on the server. Do not place it in templates, JavaScript, public configuration, screenshots, or this repository.

Without a provider key, Astra uses its built-in knowledge/rule mode. This fallback can answer selected Astra-related questions, but it is not a full generative AI model. Configure and test a provider before describing live generative AI as enabled. Review the provider's privacy terms and data-handling requirements before sending member messages to an external service.

Optional Google and GitHub sign-in

Configure OAuth applications with the production callback URLs below, replacing "YOUR-DOMAIN" with the real host:

https://YOUR-DOMAIN/accounts/google/login/callback/
https://YOUR-DOMAIN/accounts/github/login/callback/

Then set the matching client ID and secret environment variables. New social registrations use Astra's Terms and Privacy consent flow.

Optional SMTP email

By default, contact-form emails are written to the console. To deliver them through SMTP, set:

DJANGO_EMAIL_BACKEND=smtp
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_HOST_USER=your-sender@example.com
EMAIL_HOST_PASSWORD=your-provider-app-password
CONTACT_EMAIL=your-destination@example.com

Use an email-provider app password or supported credential, not your normal account password. Store it only in the server environment.

Django Admin

Open "/admin/" and sign in with an authorised staff or superuser account.

Key management areas include:

- Astragram: review posts and comments, hide or restore content, pin posts, and inspect message records where authorised.
- Rank: review proof submissions and approve or reject them; approved submissions contribute to Rank points.
- Awards: inspect competition history and generated period awards.
- Events: create and schedule celebrations; configure the effect library separately. Each event supports up to three enabled visual effects.
- Home / Gallery / Music / News: manage content and uploaded media through their respective admin sections.

Image previews are provided for supported media fields, including Astragram post images, Rank proof images, profile images, News images, home slides, Gallery images, and Music covers.

Close completed Awards periods

To finalise completed competition periods and create missing award records, run:

python manage.py close_competitions

Schedule this command periodically on the production host (for example, daily) if you want period records to be finalised without waiting for a visitor to open the Awards page.

Superuser rotation

Astra includes an explicit management command for a carefully controlled superuser rotation:

python manage.py rotate_astra_superuser

Use this only after taking and verifying a production database backup. The command asks for a replacement username, email, and password, checks whether old superuser accounts own related content, and requires the exact confirmation phrase "ROTATE-ASTRA-SUPERUSER". It creates the replacement first and stops if deleting an old account could cascade-delete protected content. Verify that the new account can sign in before treating the rotation as complete.

Database and safe upgrades

The source repository does not include a production database or uploaded user media. The default local database is SQLite, but production deployments should keep the database and media in stable locations outside disposable code-release folders.

Set "DJANGO_DB_PATH" and "DJANGO_MEDIA_ROOT" to persistent absolute paths. Ensure the hosting account has permission to read and write those paths.

For every update:

1. Back up the database file and the complete media directory.
2. Deploy the new source code without deleting or replacing those persistent locations.
3. Confirm "DJANGO_DB_PATH" and "DJANGO_MEDIA_ROOT" still point to the correct existing paths.
4. Install any updated requirements.
5. Run "python manage.py migrate".
6. Run "python manage.py collectstatic --noinput".
7. Reload the web application and verify the main features.

Never delete the production database, uploaded media, or migration history during a routine code update. Django migrations should be applied to the existing database after a verified backup; do not replace it with a database from a source archive.

Deployment notes

Astra is a standard Django project and can be deployed to a Django-compatible host, including PythonAnywhere.

For a production deployment:

- Set a strong private "DJANGO_SECRET_KEY".
- Set "DJANGO_DEBUG=False" and configure "DJANGO_ALLOWED_HOSTS" with the actual domain.
- Configure HTTPS and, where appropriate, "DJANGO_SECURE=True" and "DJANGO_HTTP_PROTOCOL=https".
- Keep the database and media directories persistent and outside disposable release directories.
- Run migrations and collect static files after deploying code.
- Configure the host's static-file mapping for "/static/" to the collected "STATIC_ROOT" directory.
- Configure the host's media mapping for "/media/" to the persistent "DJANGO_MEDIA_ROOT" directory. Django's development media route is not a production media server.
- Reload the web application after configuration changes.

For PythonAnywhere, configure the WSGI file to point to the deployed project and virtual environment, set the required environment variables, and add "/static/" and "/media/" mappings in the Web tab. The media mapping must point to the same persistent directory configured as "DJANGO_MEDIA_ROOT".

SEO and discoverability

Astra v11 includes:

- "sitemap.xml" for intended public pages and published articles.
- "robots.txt" rules that keep private account, administration, messaging, and submission routes out of general crawling.
- Separate environment controls for OAI-SearchBot and GPTBot.
- "llms.txt" as an optional plain-language map of public pages.
- Page-level SEO context, canonical and social-sharing metadata where configured.

Google Search Console

1. Verify ownership of the live domain in "Google Search Console" (https://search.google.com/search-console).
2. If using HTML-tag verification, set "GOOGLE_SITE_VERIFICATION" on the server and complete verification.
3. Submit "https://YOUR-DOMAIN/sitemap.xml" in the Sitemaps section.
4. Use URL Inspection to request crawling of the homepage or another important public page.
5. Review the indexing reports over time.

A sitemap and a crawl request help discovery; they do not guarantee that Google will index a URL or show it in search results. Likewise, crawler access and "llms.txt" do not guarantee AI-platform indexing, citations, or recommendations. Choose crawler settings deliberately and review the current policies of each provider before changing them.

Security and privacy

- Never commit API keys, OAuth secrets, SMTP credentials, production database files, or private uploaded media.
- Keep "DJANGO_DEBUG=False" on a public production site.
- Use HTTPS and a private random Django secret key.
- Back up the database and media before migrations or account maintenance.
- Review and customise the Terms and Privacy pages to match the actual hosting, authentication, email, analytics, AI-provider, retention, and data-processing setup before public launch. The included policy pages are project drafts, not legal advice.
- If a live AI provider is enabled, explain the relevant third-party data processing to members and follow the provider's applicable terms.

License

No "LICENSE" file is included in this source package yet. Until the project owner adds a license, do not assume that the source may be redistributed, modified, or used commercially.

Validation status

The source package includes Django tests and migrations for the v11 workflows. During packaging, Python syntax compilation and JavaScript syntax checks were completed, and the ZIP archive integrity was checked.

The packaging environment did not have Django and django-allauth installed. Therefore, the Django system check, migrations against a real database, automated Django test suite, and deployed-browser checks were not run as part of packaging. Run the following in your own installed environment before production release:

python manage.py check
python manage.py migrate
python manage.py test

After deployment, manually verify login, profiles, follow/unfollow, Astragram, direct messages, News, Astra AI, Rank submissions, Awards claims, Events, uploaded-image previews, Music, Gallery, and Mini Games at desktop and mobile widths.

Roadmap

Astra is an evolving project. Future work may expand the AI experience, community tools, content discovery, administration workflows, and integrations while preserving user data and the platform's modular structure.

Connect

- Astra Land: "astrarya11.carrd.co" (https://astrarya11.carrd.co)
- GitHub: "a7rya1390-ux" (https://github.com/a7rya1390-ux)
- X: "@ASTRArya11" (https://x.com/ASTRArya11)
- Instagram: "@astra_201105" (https://www.instagram.com/astra_201105/)
- Telegram: "Astra" (https://t.me/Astra_1105)
- LinkedIn: "Astra / project profile" (https://www.linkedin.com/in/arya-ghavami-4ba5a23a3/)

---

<div align="center">
  <strong>ASTRA v11</strong><br />
  <em>Build with purpose. Connect ideas. Keep moving forward.</em>
</div>
