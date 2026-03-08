# Remotion Skill per Claude Code

Una skill completa per [Claude Code](https://docs.anthropic.com/en/docs/claude-code) con **37 regole specializzate**, **template professionali per social media**, **5 temi**, **componenti pronti all'uso** e un **team di 4 agenti** per [Remotion](https://remotion.dev) - il framework per creare video con React.

A comprehensive Claude Code skill with **37 specialized rules**, **professional social media templates**, **5 themes**, **ready-to-use components** and a **team of 4 agents** for [Remotion](https://remotion.dev) - the framework for creating videos programmatically in React.

---

## Cosa fa questa skill?

Quando la attivi, Claude Code diventa un esperto completo di Remotion. Sa tutto su:

### Regole fondamentali (37 rules)
- **Safe zone per Instagram Reels** - i margini obbligatori per il formato 9:16
- **Dimensioni font per social media** - le dimensioni minime leggibili per post e reel
- **Verifica testi italiani** - controllo automatico degli accenti e degli apostrofi
- **37 regole** che coprono animazioni, audio, video, sottotitoli, transizioni, 3D, grafici, mappe e molto altro
- **3 componenti di esempio** pronti all'uso (grafico a barre, macchina da scrivere, evidenziazione parole)

### Pro Studio (template e componenti)
- **Decision engine** - scelta automatica di formato, template e tema in base alla richiesta
- **8 template** pronti (4 post + 4 reel): Carousel, Quote, Product, Announcement, Showcase, Testimonial, Tutorial, Countdown
- **5 temi** (default, luxury, modern, vibrant, minimal) con colori e font coordinati
- **Componenti** per animazioni, effetti, testo, transizioni, UI e layout
- **Checklist domande pre-video** - domande che Claude pone all'utente prima di iniziare

### Team di 4 agenti specializzati

| Agente | Ruolo | Cosa fa |
|---|---|---|
| `team-lead` | Coordinatore | Orchestrazione, code review, architettura |
| `animation-architect` | Motion designer | Springs, easings, transizioni, performance |
| `template-builder` | Sviluppatore | Template posts/reels, layout, scene system |
| `visual-effects` | VFX specialist | Effetti, temi, text animations, icone |

## Pacchetti Remotion coperti

Questa skill copre tutto l'ecosistema Remotion:

```
remotion                        # Core - il cuore del framework
@remotion/cli                   # CLI (studio per anteprima, render per esportare)
@remotion/media                 # Componenti Video e Audio
@remotion/google-fonts          # Google Fonts (caricamento automatico)
@remotion/fonts                 # Font locali (woff2, ttf, ecc.)
@remotion/transitions           # Transizioni: fade, slide, wipe, flip, clock-wipe
@remotion/captions              # Sottotitoli stile TikTok con highlight parole
@remotion/media-utils           # Visualizzazione audio (barre, waveform)
@remotion/layout-utils          # Misura testo e adattamento automatico
@remotion/three                 # Three.js / React Three Fiber (3D)
@remotion/lottie                # Animazioni Lottie
@remotion/gif                   # GIF / APNG / AVIF / WebP animate
@remotion/paths                 # Animazione tracciati SVG (grafici a linee)
@remotion/light-leaks           # Effetti luce WebGL (transizioni)
@remotion/install-whisper-cpp   # Trascrizione audio con Whisper
@remotion/zod-types             # Parametri con Zod (color picker, ecc.)
@remotion/sfx                   # Effetti sonori pronti all'uso
```

Pacchetti esterni coperti: `mediabunny`, `mapbox-gl`, `@turf/turf`

## Installazione veloce con Claude Code

Se hai gia Claude Code, puoi installare tutto con un copia-incolla! Apri il file [INSTALL-PROMPT.md](./INSTALL-PROMPT.md), copia il prompt e incollalo in Claude Code. Lui fara tutto da solo: installera la skill, il team di agenti, creera il progetto Remotion, e aggiungera tutti i 21 pacchetti.

## Installazione passo-passo (manuale)

### Prerequisiti

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installato e funzionante
- Un progetto Remotion (o la voglia di crearne uno!)

### Se sei su Windows con WSL (consigliato)

Se usi Windows, ti consiglio di lavorare con WSL (Windows Subsystem for Linux). Ecco come:

1. **Installa WSL** (apri PowerShell come amministratore):
   ```powershell
   wsl --install
   ```

2. **Installa Node.js dentro WSL**:
   ```bash
   curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
   sudo apt-get install -y nodejs
   ```

3. **Installa Claude Code**:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

### Installare la skill

1. **Clona questo repository**:
   ```bash
   git clone https://github.com/brunotr88/TruantSkills.git
   ```

2. **Copia la skill nella directory di Claude Code**:
   ```bash
   mkdir -p ~/.agents/skills
   cp -r TruantSkills/remotion-skill-powered-by-truant ~/.agents/skills/remotion-best-practices
   ```

3. **Abilita Agent Teams** (consigliato - attiva il sistema di team collaborativo):
   ```bash
   claude config set --global env.CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS 1
   ```
   Poi riavvia Claude Code.

4. **Installa il team di agenti**:
   ```bash
   mkdir -p ~/.claude/teams/remotion-pro-studio
   cp TruantSkills/remotion-skill-powered-by-truant/team/config.json ~/.claude/teams/remotion-pro-studio/config.json
   ```

5. **Fatto!** La skill si attivera automaticamente quando lavori su un progetto Remotion.

### Creare un nuovo progetto Remotion (se non ne hai uno)

```bash
# Con npm
npx create-video@latest il-mio-video

# Con bun (piu veloce)
bunx create-video@latest il-mio-video

# Entra nella cartella e avvia
cd il-mio-video
npm start
```

Si aprira il browser con lo studio di Remotion dove puoi vedere l'anteprima dei tuoi video in tempo reale.

## Come usarla

Una volta installata, la skill si attiva da sola quando Claude Code rileva codice Remotion. Puoi anche invocarla direttamente con questi prompt di esempio:

### Prompt di esempio

```
Crea un Reel Instagram 9:16 con testo animato che rispetti le safe zone

Costruisci un grafico a barre animato con effetto spring

Aggiungi sottotitoli stile TikTok con evidenziazione della parola corrente

Crea un'animazione mappa che mostra il percorso da Roma a Milano con Mapbox

Crea un post carousel luxury per Instagram con 4 slide prodotto

Genera un reel countdown energetico con tema vibrant
```

## Struttura dei file

```
remotion-skill-powered-by-truant/
├── README.md                   # Questo file
├── SKILL.md                    # Entry point della skill (caricato da Claude Code)
├── INSTALL-PROMPT.md           # Prompt copia-incolla per installazione automatica
├── rules/                      # 37 regole Remotion
│   ├── 3d.md                   # Three.js e React Three Fiber
│   ├── animations.md           # Pattern fondamentali di animazione
│   ├── assets.md               # Import di immagini, video, audio, font
│   ├── audio.md                # Audio: trim, volume, velocita, pitch, loop
│   ├── audio-visualization.md  # Barre spettro, waveform, effetti bass
│   ├── calculate-metadata.md   # Durata e dimensioni dinamiche
│   ├── can-decode.md           # Validazione decodifica video
│   ├── charts.md               # Grafici: barre, torta, linee, azioni
│   ├── compositions.md         # Composizioni, still, cartelle, props
│   ├── display-captions.md     # Visualizzazione sottotitoli TikTok
│   ├── extract-frames.md       # Estrazione frame da video
│   ├── ffmpeg.md               # Operazioni FFmpeg/FFprobe
│   ├── fonts.md                # Google Fonts e font locali
│   ├── get-audio-duration.md   # Durata audio
│   ├── get-video-dimensions.md # Dimensioni video
│   ├── get-video-duration.md   # Durata video
│   ├── gifs.md                 # GIF, APNG, AVIF, WebP animate
│   ├── images.md               # Immagini con <Img>
│   ├── import-srt-captions.md  # Import sottotitoli SRT
│   ├── light-leaks.md          # Effetti luce WebGL
│   ├── lottie.md               # Animazioni Lottie
│   ├── maps.md                 # Animazioni mappa con Mapbox
│   ├── measuring-dom-nodes.md  # Misura elementi DOM
│   ├── measuring-text.md       # Misura e adattamento testo
│   ├── parameters.md           # Parametri Zod
│   ├── sequencing.md           # Pattern Sequence e Series
│   ├── sfx.md                  # Effetti sonori
│   ├── subtitles.md            # Sistema sottotitoli/captions
│   ├── tailwind.md             # TailwindCSS in Remotion
│   ├── text-animations.md      # Macchina da scrivere, highlight
│   ├── timing.md               # Interpolazione, spring, easing
│   ├── transcribe-captions.md  # Trascrizione con Whisper
│   ├── transitions.md          # TransitionSeries, overlay
│   ├── transparent-videos.md   # Video trasparenti (ProRes/WebM)
│   ├── trimming.md             # Taglio inizio/fine animazioni
│   ├── videos.md               # Video: trim, volume, velocita, loop
│   ├── voiceover.md            # Voiceover con ElevenLabs TTS
│   └── assets/
│       ├── charts-bar-chart.tsx            # Componente grafico a barre
│       ├── text-animations-typewriter.tsx   # Effetto macchina da scrivere
│       └── text-animations-word-highlight.tsx  # Effetto evidenziazione parole
├── references/                 # Documentazione Pro Studio
│   ├── animations.md           # Springs, easings, entrance/exit API
│   ├── components.md           # Text, effects, UI, layout, scenes API
│   ├── creating-templates.md   # Guida creazione nuovi template
│   └── team-workflow.md        # Workflow collaborativo del team
└── team/
    └── config.json             # Configurazione team 4 agenti
```

## License

[MIT](../LICENSE) - Usa, modifica e condividi liberamente.

---

*Skill creata da [Bruno Truant](https://isipc.com) - Parte della collezione [TruantSkills](https://github.com/brunotr88/TruantSkills).*
