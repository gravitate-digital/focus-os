# Sound Effects and Fun Settings: Handover for Other Apps

> Use this to add the same sound effects, display themes, and gamification to the Workflow app, Pace, or any other Gravitate app.

---

## Sound Files

All MP3 files live in `/sounds/` relative to the app root:

| File | Name | Use |
|---|---|---|
| `sounds/ding-sound-effect_2.mp3` | Ding | Clean default, task complete |
| `sounds/finish-him.mp3` | FINISH HIM! | Mortal Kombat, pairs with Scorpion animation |
| `sounds/michael-jackson-hee-hee.mp3` | Michael Jackson | Hee-hee celebration |
| `sounds/yippeeeeeeeeeeeeee.mp3` | Yippee! | Excited celebration |
| `sounds/Snoop.mp3` | Snoop Dogg | Drop it like it's hot |
| `sounds/final_fantasy_KDr5Pxg.mp3` | Final Fantasy | Victory fanfare |
| `sounds/deg-deg_4M6Cojn.mp3` | Deg Deg | Quick alert |

**Source copies on Saxon's machine:** `/Users/saxonfarnworth/Downloads/` (original filenames above)

**Deployed copies:** `https://focus-os-snowy-nu.vercel.app/sounds/FILENAME`

---

## How to Add to Another App

### 1. Copy the sounds folder

Copy `sounds/` from the Focus deploy directory into the target app's public/static directory.

### 2. Add the constants

```javascript
const SOUND_EFFECTS = [
  {id:'none',          name:'Muted',           file:null},
  {id:'ding',          name:'Ding',            file:'sounds/ding-sound-effect_2.mp3'},
  {id:'finish-him',    name:'FINISH HIM!',     file:'sounds/finish-him.mp3'},
  {id:'hee-hee',       name:'Michael Jackson', file:'sounds/michael-jackson-hee-hee.mp3'},
  {id:'yippee',        name:'Yippee!',         file:'sounds/yippeeeeeeeeeeeeee.mp3'},
  {id:'snoop',         name:'Snoop Dogg',      file:'sounds/Snoop.mp3'},
  {id:'final-fantasy', name:'Final Fantasy',   file:'sounds/final_fantasy_KDr5Pxg.mp3'},
  {id:'deg-deg',       name:'Deg Deg',         file:'sounds/deg-deg_4M6Cojn.mp3'},
];
```

### 3. Add the play function

```javascript
let currentPreviewAudio = null;

function playTaskSound(soundId) {
  const sfx = SOUND_EFFECTS.find(s => s.id === soundId);
  if (!sfx || !sfx.file) return;
  if (currentPreviewAudio) { currentPreviewAudio.pause(); currentPreviewAudio = null; }
  const audio = new Audio(sfx.file);
  audio.volume = 0.5;
  currentPreviewAudio = audio;
  audio.play().catch(() => {});
  audio.addEventListener('ended', () => { if (currentPreviewAudio === audio) currentPreviewAudio = null; });
  
  // Show FINISH HIM animation if that sound is selected
  if (soundId === 'finish-him') showFinishHim();
}
```

### 4. Call it on task completion

Wherever a task/ticket/item is marked as done:
```javascript
playTaskSound(userSettings.soundEffect || 'ding');
```

### 5. Add settings UI

Render the sound effects as a grid of buttons. Clicking one plays a preview and saves the selection. Include a mute toggle.

---

## Display Themes

Six themes defined by CSS custom properties via `[data-display]` attribute on `<body>`:

| ID | Name | Vibe | Key Colors |
|---|---|---|---|
| `default` | Default | Clean midnight glass | #050a14, #6aa7ff |
| `ivory` | Ivory | Light Gravitate cream | #FAF9F6, #0048AD |
| `leather` | Leather | Dark cocoa warmth | #0F0907, #6DAAFF |
| `ocean` | Ocean Blue | Deep navy glass | #00193D, #6DAAFF |
| `arcade` | Arcade | Neon magenta + cyan | #0a0014, #ff00ff, #00ffff |
| `retro` | Retro Game | Classic game UI | #1a1c2c, #41a6f6 |

Apply by setting: `document.body.dataset.display = 'arcade';`

Each theme overrides CSS variables: `--bg, --tx, --mu, --dim, --line, --accent, --glass-bg, --glass-bo, --glass-hi`

---

## FINISH HIM! Animation (CSS only, no video)

The animation is pure CSS: Scorpion emoji enters from left, chain extends across screen, spear flies to center, screen flashes white, then "FINISH HIM!" slams in with a red glow. "GET OVER HERE" subtitle fades in below. Total duration: 2.2 seconds.

Copy the CSS classes starting with `.finish-him-overlay` and the JS function `showFinishHim()`.

---

## Arcade Mode Gamification

When `displayTheme === 'arcade'`:
- Uncompleted tasks slowly grow in size (CSS animation over 30 min) pressuring completion
- Dock items glow neon on hover
- Clock gets a text-shadow glow
- All glass surfaces tint magenta

---

## For Workflow App Specifically

The workflow app (design handoff at `~/Downloads/design_handoff_workflow_os/`) can use this system by:

1. Copying `sounds/` into the Workflow public directory
2. Adding the `SOUND_EFFECTS` constant and `playTaskSound()` to its JS
3. Calling `playTaskSound()` when a workflow task/card is completed
4. Adding the theme CSS to its stylesheet
5. Adding the settings panel for sound and theme selection

The state shape additions needed:
```javascript
// Add to the app's persisted state
soundEffect: 'ding',    // which sound to play
soundMuted: false,       // global mute
displayTheme: 'default', // visual theme
```

---

*Focus: The space where it all happens.*
