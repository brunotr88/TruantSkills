# Prompt di installazione - Remotion Skill + Team

Copia e incolla il prompt qui sotto direttamente in Claude Code.
Claude si occupera di tutto: installare la skill, configurare il team di agenti, creare il progetto, aggiungere tutti i pacchetti.

**IMPORTANTE:** Prima di incollare il prompt, attiva la modalita Plan in Claude Code digitando `/plan` oppure premendo `Shift+Tab` per passare a Plan mode. Questo fa si che Claude analizzi tutto il piano prima di eseguirlo, evitando errori.

---

## Prompt da copiare

```
Avvia in plan mode: analizza prima tutto il piano, poi esegui.
Utilizza sequential-thinking per pianificare ed eseguire questa installazione in modo ordinato.
Crea un team di agenti dedicato per parallelizzare le operazioni dove possibile.

Esegui queste operazioni in sequenza. Non chiedere conferma, procedi automaticamente.

### STEP 1: Abilita Agent Teams (sistema di team collaborativo)

Esegui questo comando per abilitare il sistema di team con TeamCreate, TaskCreate e SendMessage:

claude config set -g env.CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS 1

IMPORTANTE: Dopo questo comando, riavvia Claude Code perche la variabile d'ambiente venga caricata.
Se non puoi riavviare ora, il team funzionera comunque in modalita fallback con il tool Agent standard.

### STEP 2: Clona il repository TruantSkills

git clone https://github.com/brunotr88/TruantSkills.git /tmp/TruantSkills

### STEP 3: Installa la skill Remotion

Copia la skill completa nella directory di Claude Code:

mkdir -p ~/.agents/skills
cp -r /tmp/TruantSkills/remotion-skill-powered-by-truant ~/.agents/skills/remotion-best-practices

La skill include:
- 37 regole fondamentali di Remotion (rules/)
- Template professionali, animazioni, effetti, temi (references/)
- Checklist domande pre-video
- Decision engine per formato/template/tema

Verifica che la skill sia installata controllando che esista:
- ~/.agents/skills/remotion-best-practices/SKILL.md

### STEP 4: Installa il team di 4 agenti specializzati

Copia la configurazione del team nella directory teams di Claude Code:

mkdir -p ~/.claude/teams/remotion-pro-studio
cp /tmp/TruantSkills/remotion-skill-powered-by-truant/team/config.json ~/.claude/teams/remotion-pro-studio/config.json

Il team include 4 agenti:
- team-lead: coordinamento, code review, architettura
- animation-architect: springs, easings, transizioni, motion design
- template-builder: template posts/reels, layout, scene system
- visual-effects: effetti (grain, particles, glow), temi, text animations

Verifica che il team sia installato controllando che esista:
- ~/.claude/teams/remotion-pro-studio/config.json

### STEP 5: Pulizia repository temporaneo

rm -rf /tmp/TruantSkills

### STEP 6: Crea la cartella progetti e il progetto Remotion

Crea la cartella C:\PROGETTI se non esiste gia, poi crea dentro una sottocartella dedicata a Remotion:

mkdir -p /mnt/c/PROGETTI/remotion
cd /mnt/c/PROGETTI/remotion
npx create-video@latest remotion-studio
cd remotion-studio

### STEP 7: Installa TUTTI i pacchetti Remotion

Installa l'ecosistema completo di pacchetti Remotion. Usa il package manager gia presente nel progetto (controlla se esiste bun.lock, package-lock.json, yarn.lock o pnpm-lock.yaml).

Ecco la lista completa. Usa "npx remotion add" per i pacchetti @remotion/* (garantisce compatibilita versioni):

npx remotion add @remotion/animated-emoji
npx remotion add @remotion/animation-utils
npx remotion add @remotion/captions
npx remotion add @remotion/fonts
npx remotion add @remotion/gif
npx remotion add @remotion/google-fonts
npx remotion add @remotion/layout-utils
npx remotion add @remotion/light-leaks
npx remotion add @remotion/lottie
npx remotion add @remotion/media
npx remotion add @remotion/media-utils
npx remotion add @remotion/motion-blur
npx remotion add @remotion/noise
npx remotion add @remotion/paths
npx remotion add @remotion/player
npx remotion add @remotion/sfx
npx remotion add @remotion/shapes
npx remotion add @remotion/three
npx remotion add @remotion/transitions
npx remotion add @remotion/zod-types
npx remotion add @remotion/install-whisper-cpp

Pacchetti third-party utili (installa con npm/bun/yarn):

npm install zod lucide-react react-icons

IMPORTANTE: Usa "npx remotion add" per i pacchetti @remotion/* (garantisce compatibilita versioni). Usa npm/bun/yarn install per i pacchetti non-remotion.

### STEP 8: Verifica installazione completa

1. Controlla che tutti i pacchetti siano nel package.json
2. Conferma che la skill e installata
3. Conferma che il team di 4 agenti e configurato
4. Avvia lo studio Remotion con "npm run dev" per verificare che tutto funzioni

### STEP 9: Riepilogo

Mostra un riepilogo finale di cosa e stato installato:
- Numero pacchetti Remotion installati nel progetto
- Path della skill installata
- Nome del team e i 4 agenti disponibili
- Path del progetto: C:\PROGETTI\remotion\remotion-studio\
- Comando per avviare lo studio: npm run dev (apre il browser con anteprima live)
- Comando per esportare un video: npx remotion render <CompositionId> output.mp4
- Comando per aggiornare Remotion: npx remotion upgrade
- Il team di agenti si attiva automaticamente quando chiedi di creare un video
```

---

## Come usare questo prompt

1. Apri un terminale (WSL su Windows, o terminale su Mac/Linux)
2. Avvia Claude Code con `claude`
3. Attiva **Plan mode**: digita `/plan` oppure premi `Shift+Tab` fino a vedere "Plan" nella barra in basso
4. Incolla il prompt qui sopra e premi Invio
5. Claude prima analizzerai il piano, poi ti chiedera conferma per eseguirlo
6. Il progetto verra creato in `C:\PROGETTI\remotion\remotion-studio\`

## Note importanti

- **`npx remotion add`** e il modo ufficiale per aggiungere pacchetti Remotion. Gestisce automaticamente la compatibilita delle versioni tra tutti i pacchetti.
- Se usi **bun** invece di npm, sostituisci `npx` con `bunx` in tutti i comandi.
- La skill si attiva **automaticamente** quando Claude Code rileva file `.tsx` che importano da `remotion`.
- Per **aggiornare** Remotion in futuro: `npx remotion upgrade`
- Il **team di agenti** si attiva automaticamente quando chiedi di creare un video (richiede `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`)

## Cosa viene installato - Riepilogo completo

### 1 Skill completa di Claude Code

| Skill | Cosa include |
|---|---|
| `remotion-best-practices` | **37 regole fondamentali** (animazioni, audio, video, font, safe zones, testi italiani, sottotitoli, transizioni, 3D, grafici, mappe) + **Pro Studio** (5 temi, componenti pronti, 8 template, decision engine, checklist domande pre-video) |

### 1 Team con 4 Agenti Specializzati

| Agente | Ruolo | Cosa fa |
|---|---|---|
| `team-lead` | Coordinatore | Orchestrazione, code review, architettura, assegnazione task |
| `animation-architect` | Motion designer | Springs, easings, entrance/exit, transizioni, performance |
| `template-builder` | Sviluppatore | Template posts/reels, layout, scene system, Zod schemas |
| `visual-effects` | VFX specialist | Effetti (grain, particles, glow), temi, text animations, icone |

### 21 Pacchetti Remotion

| Pacchetto | A cosa serve |
|---|---|
| `remotion` | Il cuore del framework: useCurrentFrame, interpolate, spring |
| `@remotion/cli` | Lo studio (anteprima nel browser) e il render (esporta video) |
| `@remotion/media` | Componenti `<Video>` e `<Audio>` con trim, volume, loop, pitch |
| `@remotion/google-fonts` | Carica qualsiasi Google Font in modo type-safe |
| `@remotion/fonts` | Carica font locali dal tuo computer (woff2, ttf, otf) |
| `@remotion/transitions` | Transizioni tra scene: fade, slide, wipe, flip, clock-wipe |
| `@remotion/captions` | Sottotitoli stile TikTok con evidenziazione parola per parola |
| `@remotion/media-utils` | Visualizzazione audio: barre spettro, waveform, effetti bass |
| `@remotion/layout-utils` | Misura il testo e adatta automaticamente la dimensione del font |
| `@remotion/three` | 3D con Three.js e React Three Fiber dentro i video |
| `@remotion/lottie` | Animazioni Lottie (da LottieFiles) sincronizzate al timeline |
| `@remotion/gif` | GIF, APNG, AVIF, WebP animate e sincronizzate |
| `@remotion/paths` | Anima tracciati SVG (grafici a linee, firme, percorsi) |
| `@remotion/light-leaks` | Effetti luce cinematografici WebGL per transizioni wow |
| `@remotion/install-whisper-cpp` | Trascrizione audio automatica con Whisper (genera sottotitoli) |
| `@remotion/zod-types` | Parametri video editabili nello studio (color picker, slider) |
| `@remotion/sfx` | Effetti sonori pronti: whoosh, click, shutter, page-turn |
| `@remotion/animated-emoji` | Emoji animate sincronizzate al timeline del video |
| `@remotion/animation-utils` | Utility avanzate per animazioni complesse |
| `@remotion/motion-blur` | Motion blur realistico sulle animazioni veloci |
| `@remotion/noise` | Rumore Perlin/Simplex per animazioni organiche e naturali |
| `@remotion/player` | Player React per mostrare i video dentro una web app |
| `@remotion/shapes` | Forme geometriche SVG animate (cerchi, rettangoli, stelle, poligoni) |

### 3 Pacchetti Third-Party

| Pacchetto | A cosa serve |
|---|---|
| `zod` | Schema validation per rendere i video parametrizzabili |
| `lucide-react` | Icone SVG moderne e leggere |
| `react-icons` | Mega-libreria con migliaia di icone (Font Awesome, Material, ecc.) |
