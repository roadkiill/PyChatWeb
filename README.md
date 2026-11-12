# PyChat Web — Guest Edition

A browser-based guest client for PyChat. The UI is split into separate HTML, CSS, and JavaScript files.

## Files
- `index.html` — page structure
- `styles.css` — styling
- `app.js` — Firebase guest authentication, rooms, messages, room settings and UI behavior
- `firebase-config.example.js` — safe template for Firebase's public web-app configuration
- `README.md` — setup notes

## Firebase setup
1. In Firebase Console, open your existing PyChat project.
2. Register a Web App (if you have not already).
3. Enable **Authentication → Sign-in method → Anonymous**.
4. Copy `firebase-config.example.js` to `firebase-config.js`.
5. Fill in the Firebase Web App config values from Project settings → Your apps.
6. Serve this folder from `localhost` or an HTTPS host. Firebase Auth and microphone access require a secure context (localhost is okay for development).

`firebase-config.js` is intentionally not included in the ZIP. The app will not connect until you create it.

### About Firebase credentials
Firebase's browser `apiKey`, `authDomain`, `databaseURL`, `projectId`, and app IDs are public client configuration; a browser must know them to connect. They are not admin credentials. Actual protection comes from Firebase Authentication and Realtime Database Security Rules. Never put a service-account key, private key, or admin SDK credentials in this folder.

Use the database rules from your existing desktop project as the starting point, and test them carefully. The browser app uses anonymous auth only. It does not implement Google sign-in, username reservation, friend lists, friend requests, or account management; those options direct users to install the desktop app.

## Run locally
From this folder, start a static server, for example:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000`.

## Important current limitations
- Text rooms and guest presence use Firebase Realtime Database.
- Voice capture permission is exposed in the UI, but multi-user WebRTC signaling/relay is not implemented in this browser build yet. The desktop app's voice bridge is a separate local service and is not directly reusable by a hosted static web page.
- Public room browsing depends on your Firebase database rules and the `publicRooms` data structure.
- This is a client application, not a trusted server. Enforce permissions and validation in Firebase rules, not only in JavaScript.
