# Audio Skill: Sound Effects for Gravitate Apps

> Drop this into any Gravitate app (Workflow, Pace, Focus, etc) to add sound effects on actions.
> All MP3 files live in the `sounds/` directory. Copy the whole folder.

---

## File Locations

**Desktop:** `/Users/saxonfarnworth/Desktop/Gravitate Focus/sounds/`
**Deployed:** `https://focus-os-snowy-nu.vercel.app/sounds/`
**Repo:** `https://github.com/gravitate-digital/focus-os/tree/main/sounds`

---

## Audio Categories and When to Use

### Task Completion (play when a task/ticket is marked done)

| File | Name | Best for |
|---|---|---|
| `ding-sound-effect_2.mp3` | Ding | Default, clean, professional |
| `jurassic-park-celebration.mp3` | Jurassic Park | Big milestone completed |
| `crowd-applause-cheer-small-group_tUQjCQt.mp3` | Crowd Applause | Team win, shared achievement |
| `road-rash-64-first-place.mp3` | Road Rash Win | Finishing first, winning |
| `michael-jackson-hee-hee.mp3` | Michael Jackson | Quick celebration |
| `yippeeeeeeeeeeeeee.mp3` | Yippee | Excited, small win |
| `Snoop.mp3` | Snoop Dogg | Cool, laid back celebration |
| `final_fantasy_KDr5Pxg.mp3` | Final Fantasy | Victory fanfare, RPG style |

### Kill Streaks (play when multiple tasks done in quick succession)

| File | Name | Trigger |
|---|---|---|
| `halo-1-double-kill.mp3` | Double Kill | 2 tasks done within 10 min |
| `halo-reach-3-triple-kill.mp3` | Triple Kill | 3 tasks |
| `overkill.mp3` | Overkill | 4 tasks |
| `halo-reach-killing-spree.mp3` | Killing Spree | 5 tasks |
| `extermination.mp3` | Extermination | 6 tasks |
| `killjoy.mp3` | Killjoy | 7 tasks |
| `juggernaut_aOeUFTi.mp3` | Juggernaut | 8 tasks |
| `invincible_Gud6aoH.mp3` | Invincible | 9 tasks |
| `perfection_joIshZa.mp3` | Perfection | 10 tasks |
| `halo-reach-unfrigginbelievable-voice.mp3` | Unfrigginbelievable | 15+ tasks |

### Daily Intro (play on first load of the day)

| File | Name | Best for |
|---|---|---|
| `game_over.mp3` | Game Over | Halo theme: "yesterday's over, new game" |
| `play_ball.mp3` | Play Ball | Gaming theme: "let's go" |
| `well-well-well-how-the-turntables.mp3` | How the Turntables | The Office theme: daily opener |
| `jurassic-park-celebration.mp3` | Jurassic Park | Celebration theme: start big |

### Timer Warning (play at 5 minutes remaining)

| File | Name | Best for |
|---|---|---|
| `five_mins_remaining.mp3` | 5 Minutes Remaining | Focus timer warning |
| `deg-deg_4M6Cojn.mp3` | Deg Deg | Quick alert nudge |

### Timer Complete (play when focus session ends)

| File | Name | Best for |
|---|---|---|
| `halo_3_piano_chord.mp3` | Halo Piano Chord | All priorities done, session complete |
| `teamate_gained.mp3` | Teammate Gained | Session complete, team vibes |

### Comedy / Banter (play for overdue tasks, missed deadlines, fun moments)

| File | Name | Best for |
|---|---|---|
| `finish-him.mp3` | FINISH HIM | Overdue task that needs doing |
| `nooo-god-0.mp3` | Michael: NOOO GOD | Task went wrong, deadline missed |
| `parkour-parkour-the-office-us-192-kbps_1_0.mp3` | PARKOUR! | Smashing through backlog |
| `the-office-theme-song_01.mp3` | Office Theme | Light moment, daily vibes |
| `the-office-hotdogs.mp3` | Office Hotdogs | Random celebration |
| `road-rash-64-last-place.mp3` | Road Rash Lose | Missed target, banter |
| `youre-a-noob.mp3` | You're a Noob | Friendly trash talk |
| `rpreplay_final1614990347.mp3` | Random Funny | Random chaos |

---

## How to Add to Any App

### 1. Copy the sounds folder
```bash
cp -r /Users/saxonfarnworth/Desktop/Gravitate\ Focus/sounds/ YOUR_APP/sounds/
```

### 2. Add the play function
```javascript
let currentAudio = null;

function playSound(file, volume) {
  if (currentAudio) { currentAudio.pause(); currentAudio = null; }
  const audio = new Audio(file);
  audio.volume = volume || 0.5;
  currentAudio = audio;
  audio.play().catch(() => {});
  audio.addEventListener('ended', () => { if (currentAudio === audio) currentAudio = null; });
}
```

### 3. Trigger on events
```javascript
// Task completed
playSound('sounds/ding-sound-effect_2.mp3');

// Kill streak (2+ tasks in 10 min)
playSound('sounds/halo-1-double-kill.mp3');

// Overdue task banter
playSound('sounds/finish-him.mp3');

// Daily intro
playSound('sounds/game_over.mp3', 0.4);

// Timer warning
playSound('sounds/five_mins_remaining.mp3', 0.5);
```

### 4. Show visual overlay (optional)
```javascript
function showOverlay(text, color) {
  const el = document.createElement('div');
  el.style.cssText = 'position:fixed;inset:0;z-index:9999;display:flex;align-items:center;justify-content:center;background:rgba(0,0,0,.7);opacity:0;transition:opacity .2s';
  el.innerHTML = '<div style="font-size:60px;font-weight:900;color:'+color+';text-shadow:0 0 40px '+color+'">'+text+'</div>';
  document.body.appendChild(el);
  requestAnimationFrame(() => el.style.opacity = '1');
  setTimeout(() => { el.style.opacity = '0'; setTimeout(() => el.remove(), 400); }, 1800);
}

// Usage
showOverlay('DOUBLE KILL', '#6DAAFF');
showOverlay('FINISH HIM!', '#ff2200');
```

---

*Use across Focus, Workflow, Pace, and any future Gravitate app.*
