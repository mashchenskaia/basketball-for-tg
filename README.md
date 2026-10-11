# basketball-for-tg 🏀

Swipe-to-shoot basketball game for Telegram Mini Apps. Score as many baskets as you can in 45 seconds, then challenge a friend to beat your score.

## How to play

- Swipe the ball toward the hoop. A faster swipe throws higher, and the swipe direction sets the aim.
- You have 45 seconds to score as many baskets as you can.
- A clean shot that doesn't touch the rim shows "Крууууть". A shot that hits the rim and still goes in shows "В яблочко!" or "Прямо в цель!".
- At the end, tap "Вызвать друга" to send your score to a friend in any Telegram chat. They open the link, see your score as their target, and try to beat it.

## Features

- Single HTML file with no build step and no dependencies
- Pseudo-3D ball flight with rim bounces
- Personal best saved on the device
- Friend challenges through Telegram deep links (`startapp` parameter)
- Haptic feedback inside Telegram
- Works in a regular browser too, for testing

## Setup

### 1. Host the game

This repo is set up for GitHub Pages:

1. Go to **Settings → Pages**.
2. Under **Branch**, select `main` and click **Save**.
3. The game will be live at `https://<your-username>.github.io/basketball-for-tg/`.

### 2. Create the bot and Mini App

1. In Telegram, open [@BotFather](https://t.me/BotFather) and send `/newbot` to create a bot.
2. Send `/newapp`, choose your bot, and fill in the title, description and a 640×360 image.
3. Paste the GitHub Pages URL from step 1 as the Web App URL.
4. Choose a short name (for example `game`). BotFather gives you a link like `https://t.me/<your_bot>/game`.

### 3. Set the app link

In `index.html`, replace the placeholder with your link from BotFather:

```js
const APP_LINK = 'https://t.me/YOUR_BOT/YOUR_APP';
```

Commit the change. GitHub Pages updates within a minute or two.

## How challenges work

After a round, the game builds a link like:

```
https://t.me/<your_bot>/game?startapp=c17
```

Telegram passes `c17` to the game as `start_param`, and the game shows "Цель: 17" to the player who opened it. There is no server: the score travels inside the link.

## Limitations

- Because the score is part of the link, it can be edited by hand. For honest scores and leaderboards, scores need to be stored and checked on a server (for example Supabase), with the Telegram `initData` signature verified on the backend.
- The personal best is stored in the browser's local storage, so it doesn't sync between devices.

## Tech

- HTML5 Canvas and vanilla JavaScript
- [Telegram Mini Apps API](https://core.telegram.org/bots/webapps) (`telegram-web-app.js`)
- Fonts: Russo One and Rubik from Google Fonts
