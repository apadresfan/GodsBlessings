# God's Blessings
An Instagram-inspired, responsive faith community: email accounts, verification, password reset, public blessing feed, optional compressed photos, categories, search, personal feed, Amen reactions, deletion and reporting. Warm pink, sage, and ivory.

## What works now
Without configuration, this is an explicitly labeled demo. Demo posts and identity live only in this browser; no passwords are collected. Run a local web server (`python3 -m http.server 8000` in this folder), then visit http://localhost:8000. Do not open index.html directly: browsers restrict module scripts over file URLs.

## Real accounts and shared posts
1. At https://console.firebase.google.com create a project for this site and register a Web app.
2. Enable Authentication > Sign-in method > Email/Password.
3. Create a Cloud Firestore database. Choose production/locked mode, then replace its rules with the entire contents of `firestore.rules` and publish them BEFORE connecting the website.
4. Copy the web app's Firebase configuration object into `config.js`, replacing `null`. These web identifiers are public. Never use an Admin SDK/service-account key in the site.
5. Add `YOUR-USERNAME.github.io` to Authentication > Settings > Authorized domains. Add localhost separately if testing locally.
6. Customize the verification and password-reset email templates. Register, verify the email, sign out and back in, then post.
7. Test with two real accounts in separate browsers: see each other's posts; confirm that each can delete only their own; submit a report and review it in Firestore. Confirm unauthenticated writes and unverified writes are rejected using the Firebase Rules Playground. Backend integration has not been tested against a provisioned project in this delivery.

## GitHub Pages
1. Create a new repository named `gods-blessings` in your GitHub account. The available connector cannot create repositories or enable Pages, so these two steps require your GitHub settings.
2. Upload the contents of this folder (not the outer folder) to the repository's main branch. Include the empty `.nojekyll` file.
3. Open Settings > Pages > Deploy from a branch > main > /(root) > Save.
4. GitHub supplies the exact URL, normally https://YOUR-USERNAME.github.io/gods-blessings/ . Wait for deployment before sharing it.
No build or package installation is required.

## Photos, costs and launch limits
Photos are resized and stored as small JPEG strings inside Firestore documents, capped below 180,000 characters. This avoids requiring Firebase Storage for the first version but is not suitable for large-scale photo sharing. Firebase quotas and pricing can change: review current Firebase pricing and usage before launch; do not assume unlimited free operation. No paid services are enabled by this code.
All stories and photos are public, even when the visitor is signed out. Emails remain in Firebase Authentication and are not put in public posts. The display name is self-chosen, not verified identity.
Reports are stored privately for the project owner to review in the Firebase console; there is no automatic email notification or moderation dashboard. The project owner can delete reported posts through the console. An optional trusted server can assign an `admin` custom claim, but never do this in client code. Deleting a post does not delete its reaction subcollection; clean up orphaned reaction documents in the console or through a trusted backend.
This initial version does not include follows, comments, direct messaging, profile editing, or automated abuse/rate limiting. Before inviting a large public audience, add App Check, spam controls, moderation procedures, and your contact/privacy information. Do not publish private details about other people without permission.

## Validation
HTML parsed; JavaScript syntax checked; static file references and archive contents checked. Browser visual QA and live Firebase integration were not available in the build environment. No claim of live deployment is made.
