<div align="center">

<img src="docs/assets/SafePathLogo.svg" alt="SafePath logo" width="96" />

# SafePath

**Community-powered urban safety navigation — see it, report it, route around it.**

SafePath turns real-time, crowd-sourced safety reports into a live risk map and an A*-powered
"safest route" engine for drivers, walkers, and cyclists. Built with Flutter + Firebase.

[![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?logo=flutter&logoColor=white)](https://flutter.dev)
[![Firebase](https://img.shields.io/badge/Firebase-Auth%20%7C%20Firestore-FFCA28?logo=firebase&logoColor=black)](https://firebase.google.com)
[![OSRM](https://img.shields.io/badge/Routing-OSRM%20%2B%20A*-2f855a)](http://project-osrm.org)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Android%20%7C%20Web-informational)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[Landing Page](https://safepathco.app) · [Report a bug](https://github.com/<tyna71>/<SafePath>/issues) · [Request a feature](https://github.com/<tyna71>/<SafePath>/issues)

<img src="docs/assets/demo.gif" alt="SafePath demo" width="720" />

</div>

---

## Why SafePath?

Existing map apps can get you somewhere fast — they don't tell you whether the road is
*actually* safe to walk at night. SafePath fixes that with a simple loop:

1. **People report** an area as safe/unsafe with tags, a rating, and an optional note.
2. **Reports feed a live grid** covering the whole city, decayed over time and weighted by
   reporter trust.
3. **The router (A\* + OSRM)** scores every road segment against that grid and returns the
   safest, most balanced, or fastest route — not just the shortest one.

It's Waze for personal safety, gamified like a fitness app, and built entirely on a
free-tier-friendly stack.

## Features

| Category | Highlights |
|---|---|
| 🗺️ **Live safety map** | OpenStreetMap tiles, animated safety markers, snap-to-road reporting, light/dark themes |
| 🧭 **Safest-route engine** | Custom A* over a live risk grid + OSRM, 3 strategies (safest / balanced / fastest), turn-by-turn navigation |
| 📍 **Granular reporting** | Point → street → neighborhood → district → city scope, 25+ safety tags, star rating, anonymous mode |
| 🧑‍🤝‍🧑 **Social layer** | Friends, friend requests, public profiles, comments & likes on reports |
| 🏆 **Gamification** | XP, 25+ badges (5 rarity tiers), levels, daily quests, streaks |
| 🔔 **Smart notifications** | Proximity alerts for nearby reports, friend activity, in-app + push |
| 🤖 **AI safety assistant** | Natural-language Q&A grounded in the community's own report data |
| 🌐 **Web landing page** | https://safepathco.app — React/Vite/Tailwind, 5 languages, animated hero |

## How it works

```
report submitted            grid updated              route requested
┌───────────────┐        ┌───────────────────┐        ┌──────────────────────┐
│  Flutter app  │ ────▶ │  RoadScoreService  │ ────▶ │  SafetyRouter (A*)   │
│  (report UI)  │        │  Firestore grid   │        │  + OSRM alternatives │
└───────────────┘        │  (time-decayed,   │        └──────────────────────┘
                         │  trust-weighted)  │                   │
                         └────────────────────┘                  ▼
                                                      safest / balanced / fastest route
                                                                  +
                                                        turn- by-turn navigation
```

## Tech stack

- **App:** Flutter (Dart), `flutter_map` + OpenStreetMap tiles
- **Backend:** Firebase (Auth, Firestore, Hosting, Security Rules)
- **Routing:** OSRM (routing.openstreetmap.de) + a custom A* layer for safety-weighted paths
- **Geocoding/search:** Nominatim, Overpass API
- **Web:** React, Vite, Tailwind CSS v4, Framer Motion (safepathco.app)
- **State:** Singleton `ChangeNotifier` (`AppState`)

## Get the app

SafePath is a mobile app, not a library you build locally — get it from the store:

[![Get it on Google Play](https://img.shields.io/badge/Google%20Play-Download-414141?logo=google-play&logoColor=white)](https://play.google.com/store/apps/details?id=YOUR_PACKAGE_ID)

> Also you can download from [safepathco.app](https://safepathco.app) (Landing Page).

<!--
If the app isn't published yet, replace the block above with:

## Status

🚧 SafePath is currently in private beta and launching soon on Google Play.
[Join the waitlist](https://safepathco.app) to get notified.
-->

This repository is a **showcase** of the project — architecture, design decisions, and
selected code — rather than the full production source, which stays private while the
app is live on the store.

## Project structure

```
lib/
├── screens/        # UI screens (map, routing, onboarding, profile, settings, admin…)
├── models/         # SafetyReport, UserModel, BadgeModel, RoadSegment…
├── widgets/         # Reusable UI (glass cards, markers, report modal…)
├── services/        # RoadScoreService (grid scoring)
└── safety_router.dart  # A* + OSRM routing engine
```

## Roadmap

- [ ] Apple Sign-In backend
- [ ] iOS build
- [ ] Public API for the safety grid
- [ ] Offline-first report queue

## Contributing

Contributions, issues, and feature requests are welcome — see
[`CONTRIBUTING.md`](CONTRIBUTING.md) to get started. If SafePath is useful to you,
consider giving it a ⭐, it genuinely helps other people find it.

## License

[MIT](LICENSE)
