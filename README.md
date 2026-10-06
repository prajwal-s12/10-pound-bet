# 10 Pound Bet

A gamified daily to-do list. Set your tasks for the day: finish them all by midnight and win £1, leave one undone and you owe £10 (plus a one-tap reason why).

- **Site:** https://p7212001.github.io/10-pound-bet/
- **Hosting:** GitHub Pages (static `index.html`)
- **Login + database:** Firebase Authentication (Google, email/password) and Cloud Firestore, Spark (free) plan

## Files
- `index.html` — the whole app
- `config.js` — Firebase web config (public values)
- `firestore.rules` — database security rules: each user can only access `users/{their uid}` and its `days` subcollection

## Data model
- `users/{uid}` — `{ payTo, daily: [task text], payments: [{id, at, amount, method}] }`
- `users/{uid}/days/{YYYY-MM-DD}` — `{ date, tasks: [{id, text, done, missed?, reason?, reasonTag?}], settled, outcome: won|lost|void, stake, reward }`

Days settle lazily: when a player opens the app, any earlier unsettled day is scored (all done = won, otherwise lost) and lost days prompt for reasons.
