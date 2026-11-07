# Forest Frontier

A 3D strategy game that runs in the browser. Grow a city in the forest, upgrade its walls and weapons, train an army, and conquer 30 rival civilizations, alone or with friends online.

**Play:** https://php2101.github.io/forest-frontier/

## How it's built

Everything is plain HTML and JavaScript, with no build step.

| File | What it is |
|---|---|
| `index.html` | The whole game: 3D graphics (three.js r128 from cdnjs), world, battles, UI |
| `firebase-config.js` | Firebase settings for online multiplayer (`null` = multiplayer off) |
| `database.rules.json` | Security rules for the Firebase Realtime Database |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

## Publishing

GitHub Pages serves the `main` branch from the repository root. Every push to `main` goes live in a minute or two.

## Saves

Games save in the player's browser (`localStorage`). The 💾 button gives a **save code** that backs up the game or moves it to another device; load it from the start screen.

## Multiplayer

Rooms run on Firebase Realtime Database with anonymous sign-in, so players never need an account.

- Each player writes their own state to `rooms/<code>/players/<uid>` about every 2 seconds.
- Everyone in the room reads all players' states: cities, armies, captured civilizations, and raid results.
- A raid is fought on the attacker's device; the result is posted in the attacker's state and the defender's game applies it.

Setup: create a Firebase project, enable **Authentication → Anonymous**, create a **Realtime Database**, paste `database.rules.json` into its Rules tab, then put the web app config in `firebase-config.js`.
