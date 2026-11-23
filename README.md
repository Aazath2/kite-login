# kite-login

A one-file page that hands the daily Kite login back to Aazath's Telegram bot, so nothing has to be copied.

1. The bot's "Log in to Kite" button opens Kite's own login page.
2. After the login, Kite sends the browser here with a one-time `request_token`.
3. This page opens `https://t.me/<bot>?start=<request_token>`: Telegram shows the bot chat, and START sends the token.
4. The executor on the server swaps the token for the day's session using its API secret, which never leaves the server.

The page has no secrets and sends nothing anywhere else: it reads the address, removes the token from the
browser history, and opens Telegram. The token is single-use, expires within minutes, and is useless without
the API secret. Content-Security-Policy allows only this page's own script.

Setup (once): publish this folder with GitHub Pages from a public repo `Aazath2/kite-login`, then set the
app's Redirect URL at developers.kite.trade to `https://aazath2.github.io/kite-login/`.
