# 🌀 Naruto Hand Tracking Powers ⚡

Control **Rasengan** and **Chidori** in real-time using your bare hands and a webcam.

---

## 🚀 Overview

Uses [MediaPipe Hands](https://mediapipe.dev) to track your hands at up to 21 landmarks per hand, detect open/closed gestures, and overlay Naruto-style video effects with matching audio — all running live in the browser, no backend needed.

---

## 📁 Project Structure

```
project/
├── index.html
└── assets/
    ├── naruto.mp4      # Rasengan effect
    ├── sasuke.mp4      # Chidori effect
    ├── rasengan.mp3    # Rasengan sound
    └── chidori.mp3     # Chidori sound
```

---

## 🧑‍💻 How to Use

1. Clone or download this repo
2. Place your video and audio files in the `assets/` folder
3. Open `index.html` in a modern browser (**Chrome recommended**)
4. Click **"Tap to Begin"** to grant camera + audio access
5. Open your hands in front of the webcam

> ⚠️ Must be served over a local server or HTTPS — browsers block camera access on plain `file://`. Use [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) in VS Code or run `npx serve .`

---

## 🎮 Controls

| Hand | Gesture | Effect |
|---|---|---|
| Left hand | ✋ Open | 🌀 Rasengan (Naruto) |
| Right hand | ✋ Open | ⚡ Chidori (Sasuke) |
| Either hand | ✊ Closed | Power fades out |

Effects fade in as you hold your hand open and fade out when you close it — the HUD bars at the bottom show your current power level per hand.

---

## 📋 Requirements

- 📷 Webcam
- 🌐 Chrome, Edge, or Firefox (latest)
- 📡 Internet connection (MediaPipe loads from CDN)
- 🎬 Your own `naruto.mp4`, `sasuke.mp4`, `rasengan.mp3`, `chidori.mp3` files in `assets/`

---

## ⚙️ Technical Details

- **Hand detection** — MediaPipe Hands at 1280×720, model complexity 1, 75% detection + tracking confidence
- **Gesture logic** — compares fingertip distances to PIP joints and wrist; requires 3+ extended fingers (thumb included) to count as open
- **Coordinate mapping** — landmarks are converted to screen pixels accounting for `object-fit: cover` letterboxing, so effects land exactly on your hand regardless of screen aspect ratio
- **Audio** — browser-unlocked on first tap; guarded against overlap glitch with an `onended` callback
- **Skeleton** — color-coded per hand: 🟠 orange for Rasengan, 🔵 blue for Chidori

---

## 🛠️ Troubleshooting

| Problem | Fix |
|---|---|
| Camera not working | Check browser permissions; use HTTPS or localhost |
| Effects on wrong hand | This is intentional — MediaPipe labels hands from the camera's view, which is already mirrored |
| No sound | Click the "Tap to Begin" overlay first; browsers require a user gesture before playing audio |
| Videos not showing | Confirm `assets/` contains all four files with the exact filenames above |
| Hand tracking jittery | Improve room lighting; keep your hands fully visible within the frame |