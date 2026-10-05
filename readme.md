# 🌌 Discord - Nexus Chat

![Status](https://img.shields.io/badge/status-active-23a55a)
![License](https://img.shields.io/badge/license-MIT-5865f2)
![Made with](https://img.shields.io/badge/made%20with-HTML%20%2B%20CSS%20%2B%20JS-f0b232)
![Backend](https://img.shields.io/badge/backend-Supabase-3ecf8e)

A single-file chat application that looks and feels like Discord — with real-time messaging, video calling, private channels, and everything in between. Host it anywhere, share the link, and you've got a chat room.

---

## What It Is

Nexus Chat is one HTML file that turns into a full chat platform the moment you open it. No installation, no build tools, no backend of your own to maintain. Paste your Supabase keys, drop it on any static host, and you have a working chat room that anyone with the link can join.

It's built for people who want a Discord-style chat without the Discord — for friend groups, small communities, classrooms, side projects, or just as a fun thing to tinker with. The whole app is a single file because it doesn't need to be anything else.

---

## The Idea

Most chat apps are either:
- **Too heavy** — full server infrastructure, user databases, admin panels
- **Too simple** — plain text boxes with no personality
- **Too locked-in** — tied to one platform, one account system, one way of doing things

Nexus Chat sits in the middle. It gives you the polish of a real chat app — animated avatar frames, reactions, video calls, custom themes — while running entirely on free infrastructure and shipping as a single file you can read, fork, and host anywhere.

You don't sign up. You don't log in. You pick a username, upload a picture if you want, and you're in. Your identity is stored locally, your messages sync globally, and your data lives in *your* Supabase project, not mine.

---

## What You Can Do With It

### 💬 Talk to People
A global chat room everyone shares, plus private channels you create with custom keys. Pass the key to whoever you want in, and only they get access. Messages stay until they've been unread for 30 minutes — then they quietly disappear. Reacting to a message keeps it alive, so conversations that matter stick around.

Messages support everything you'd expect: **clickable links**, **inline image previews**, **file attachments up to 10MB**, **emoji reactions**, and **deletable history**. Images click open fullscreen. Files download with one tap.

### 👤 Make It Yours
Pick a username that nobody else is using — it's checked globally, so you're never fighting someone for the same name. Names can be up to 60 characters and support Unicode, so `𝕵𝖊𝖗𝖊𝖒𝖎𝖆𝖍 𝕸𝖔𝖔𝖗𝖊` works just as well as `john42`.

Upload a profile picture and wrap it in one of **eleven avatar frames** — some glowing, some animated, some shifting like a galaxy. Your profile sticks around between visits, so you set it up once and it just works.

### 📹 See Each Other
Click the phone button next to anyone online for a **1-on-1 video call**. Click the camera icon at the top of a channel to **call everyone in that room**. Toggle your camera and mic anytime, see a live call timer, and let the layout rearrange itself as more people join.

Calls run peer-to-peer over WebRTC — no video ever touches the database, no recordings, no middleman. Just two browsers talking directly to each other.

### 🎨 Bend It to Your Taste
Open the appearance tab and change anything. Chat background, sidebar, text colors, accent — pick them with color wheels or type in hex codes. Six gradient presets are there if you don't want to choose. Everything saves per-user, so you and your friends can each have your own look without stepping on each other.

### 🔔 Never Miss a Message
When someone messages you and the tab isn't focused, you get a **desktop notification**, a soft **chime**, and a **(1)** badge on the tab title. Click the notification and you jump straight back in.

### 🐍 And There's a Snake Game
Click the top-left profile circle five times. I won't say more.

---

## What It Isn't

- **Not a Discord replacement** — it's a chat room, not a platform. No servers-of-servers, no roles, no admin tools.
- **Not private by default** — anyone with the URL and your Supabase keys can read and write messages. It's fine for a friend group; it's not fine for anything sensitive. Real privacy would require adding authentication, which this deliberately skips.
- **Not trying to be everything** — the feature list stops where it stops. Voice messages, screen sharing, message editing, DMs separate from channels — none of those are here yet. Maybe someday.
- **Not for huge groups** — video calls use mesh topology, which means every participant connects to every other participant. That caps out around 5 people before quality starts dropping. Text chat scales fine.

---

## How It Works Under the Hood

If you're the kind of person who cares:

The app has no server of its own. Everything is client-side, backed by **Supabase** — a hosted Postgres database with real-time subscriptions and broadcast channels baked in.

- **Messages, users, and channels** live in Postgres tables
- **Real-time sync** comes from Supabase's `postgres_changes` — when a row is inserted, every open client hears about it within milliseconds
- **WebRTC signaling** (the offers, answers, and ICE candidates that let two browsers find each other) runs over Supabase's Broadcast channels, which act as a lightweight pub/sub relay
- **Presence** is tracked with a 20-second heartbeat; entries older than 45 seconds get cleaned up automatically

The entire frontend is vanilla JavaScript. No React, no framework, no bundler. Just a big `<script>` tag with everything inlined. Same for the CSS — the whole Discord-inspired theme is a few hundred lines of plain styles.

This means:
- You can read the entire source in one sitting
- You can host it on any free static host (GitHub Pages, Netlify, Vercel, Cloudflare Pages)
- You can fork it and add features without learning a build system first
- You can open it directly from your filesystem if you want

---

## Who It's For

- **Friend groups** who want a private chat without the Discord baggage
- **Small communities** that just need a room, not a platform
- **Teachers or clubs** setting up a quick chat for a class or event
- **Developers** who want a working reference for Supabase + WebRTC in a single file
- **Anyone** who thinks chat apps should be simpler than they are

---

## Getting Started

The whole setup is: fork this repo, make a free Supabase project, paste two keys into the HTML, and host it. That's genuinely it. If you want the step-by-step walkthrough, see **[SETUP.md](SETUP.md)**.

---

## Built With

- **[Supabase](https://supabase.com)** — Postgres, realtime, and broadcast
- **[WebRTC](https://webrtc.org)** — peer-to-peer video and audio
- **[Inter](https://fonts.google.com/specimen/Inter)** — the UI font
- **Vanilla JS and CSS** — no frameworks, no build step

---

## License

MIT. Do whatever you want with it.

---

## A Note

This started as "what if Discord but in one file" and turned into something genuinely fun to use. If you host it and get a community running, I'd love to hear about it. If you fork it and build something cool on top, even better.

The best software is the kind you can read end to end and understand completely. That's what this is.

---

<p align="center">
  <a href="#-nexus-chat">↑ back to top</a>
</p>
