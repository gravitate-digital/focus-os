# Focus App: Complete Handover

> Everything needed to maintain, extend, or hand off Focus to another session.
> Last updated: 20 June 2026. v52. 4,700+ lines.

---

## Links

| What | URL |
|---|---|
| **Live app** | https://focus-os-snowy-nu.vercel.app |
| **Repo** | https://github.com/gravitate-digital/focus-os |
| **Desktop copy** | /Users/saxonfarnworth/Desktop/Gravitate Focus/ |
| **Downloads copy** | /Users/saxonfarnworth/Downloads/Focus OS/ |

## Files in the project

| File | Purpose |
|---|---|
| `index.html` | The entire app (single file, 4,700+ lines) |
| `fonts/Aspekta-*.ttf` | Gravitate brand font (5 weights: 400-800) |
| `photos/*.jpg` | 15 team photos for background cycling |
| `sounds/*.mp3` | 23 audio files for celebrations, streaks, timer |
| `TEAM-HANDOVER.md` | Setup guide for team members (Chrome new tab) |
| `AUDIO-SKILL.md` | Full audio categorisation table, copy-paste code for other apps |
| `SOUND-AND-FUN-HANDOVER.md` | Sound system architecture for porting to Workflow/Pace |

## Architecture

Single self-contained HTML file. No build step. No backend. No npm.

- **State**: one object `S` persisted to `localStorage` key `focos_v10`
- **Rendering**: pure functions that read `S` and write DOM
- **Persistence**: `save()` called after every state change, writes to localStorage
- **Deploy**: `git push` to GitHub, Vercel auto-deploys

## State Shape

```javascript
S = {
  wsName, light, role, departments[],
  panels[], favourites[], dockFilter, dockStyle,
  modes[], activeMode, autoMode, autoTheme,
  theme, displayTheme, bgMode, heroPos, uiScale,
  textureOverlay, photoTransition, photoCycleSpeed,
  topPriorities[], oneThingId, intentionDate,
  focus: { duration, remaining, running, sessionsToday, lastSessionDate },
  sprint, meetings[], rocks[], tasks[],
  coach: { on, sensitivity, switchCount },
  soundTheme, soundEffect, soundMuted, streaksOn, streakCount, lastStreakTime,
  bigHead, waterReminder, showQuotes,
  firstRun, switchLog[]
}
```

## Features Built

### Core
- Hero layout: clock, focus timer, priorities card, next meeting, quote
- 45 app presets across 12 categories (Gravitate's confirmed tech stack only)
- 11 department presets with correct app trees
- Multi-department onboarding (4-step: name, departments, apps, priorities)
- Daily intention gate with carry-over from yesterday
- Unlimited priorities (no cap)
- Inline task editing (double-click)
- Ad-hoc task tagging
- Share/screenshot priorities as PNG

### Navigation
- Mega-nav: department pills in topbar, hover to expand app grid
- Bottom dock: favourites strip with add button
- Command palette (Cmd+K): search apps, tasks, actions
- Keyboard shortcuts: 1-8, F, W, S, /, ?, Alt+L, Esc

### Timer
- Pomodoro: 60/30/25/15/5m presets + custom slider (1-120m)
- Click timer number to cycle durations
- 5-minute warning with audio
- Session counter per day
- Spotify link button

### Backgrounds
- Team photos (15, cycling, preload + crossfade)
- Gradient blobs (6 colour themes)
- Unicode pattern (brand symbols)
- Photo speed slider (10s-5m)
- Photo transition style (fade/slide/blur)
- Texture overlay toggle (SVG dither)

### Themes
- 6 display themes: Default, Ivory, Leather, Ocean, Arcade, Retro
- Time-aware auto-theme (morning warm, evening dark)
- Light/dark mode (Gravitate brand colours: porcelain, navy, cream)
- Apple liquid glass dock option

### Sound
- 6 sound theme packs: Clean, Halo, The Office, Celebration, Gaming, Custom
- 18 individual task completion sounds
- Kill streaks: 10 Halo levels with voice clips (Double Kill through Unfrigginbelievable)
- Daily intro sound (Game Over, Play Ball, Turntables, Jurassic Park)
- Halo piano chord on all priorities done
- Mute toggle

### Customisation (Settings)
- Display theme, background theme/mode, dock style
- Layout position (random/left/center/right)
- UI scale slider (80-120%)
- Photo cycle speed slider
- Photo transition style
- Texture overlay toggle
- Focus coach sensitivity (off/low/med/high)
- Water reminders (45-min hydration nudge)
- Kill streaks toggle
- Comical Mode (Comic Sans + growing tasks)
- Show/hide quotes
- Change departments, manage apps
- Export/import JSON, reset all

### Security
- All data in browser localStorage, nothing sent anywhere
- No cookies, no tracking, no analytics
- Asana sync noted as requiring OAuth backend (Phase 2)
- Full transparency section in settings

## Tech Stack (confirmed by Saxon)

**Core (everyone):** Google, Gmail, Google Chat, Calendar, Drive, Docs, Sheets, Meet, Asana, Loom
**AI:** ChatGPT, Claude, Claude Design, Claude Code, Copilot
**Design:** Figma, Canva, Adobe CC, Webflow
**Reporting:** Whatagraph, GA4, Search Console
**Ads:** Google Ads, Meta Ads, TikTok Ads, Bing Ads, Amazon Ads
**SEO:** SEMrush, Screaming Frog
**Email:** Klaviyo, Mailchimp, Zoho
**Social:** Instagram, Facebook, LinkedIn
**Scheduling:** Acuity
**Call Tracking:** CallRail
**Dev:** Linear
**Gravitate:** Proposals, Pace, Space, Digital, Studio, Focus

**NOT used (removed):** Slack, Notion, HubSpot

## Phase 2 (needs proper app build)

| Feature | Requirement |
|---|---|
| Asana task sync | OAuth + Next.js API route |
| Google Calendar sync | OAuth + backend |
| Whatagraph data | API integration |
| Google Chat auto-post priorities | Webhook/API |
| Cross-device sync | Supabase |
| Chrome extension (persistent widget) | Manifest v3 build |
| Grid/Minimal/Dashboard display views | CSS + render refactor |

## Team Feedback (from first trial)

| Feedback | Decision |
|---|---|
| Ad-hoc tags for unplanned work | Done in Focus. Also park for Pace. |
| Notes/journal on tasks | Park for Pace, not Focus. |
| "Replaces Notion?" | No. Focus is the launchpad, Notion is the workspace. |
| Quick task switching (10-min bursts) | Pace problem, not Focus. |
| Desktop widget (persistent timer) | Phase 2 Chrome extension. |
| Irrelevant default meetings | Fixed: empty meetings by default. |
| Irrelevant default tasks | Fixed: empty tasks by default. |
| 5-min timer warning | Done with audio. |
| Spotify link | Done. |

## Brand Rules Applied

- Aspekta font (400-800 weights)
- No em dashes (colons, commas, pipes)
- Gravitate colours: porcelain #FAF9F6, navy #00193D, cream #EDE9DE, accent #0048AD/#6DAAFF
- Where black: very dark brown (#0F0907). Where white: porcelain. Where grey: cream.
- No Slack, no orange, no generic grey
- Title case headings

## How to Deploy Changes

```bash
# Edit the file
open "/Users/saxonfarnworth/Desktop/Gravitate Focus/index.html"

# Copy to deploy directory
cp "/Users/saxonfarnworth/Desktop/Gravitate Focus/index.html" /tmp/focus-os/index.html

# Push and deploy
cd /tmp/focus-os && git add -A && git commit -m "description" && git push origin main
vercel --yes --prod
```

## How to Test Fresh

Open browser console on the app:
```javascript
localStorage.removeItem('focos_v10');
location.reload();
```

---

*Focus v52. Built by Saxon Farnworth with Claude Code. June 2026.*
