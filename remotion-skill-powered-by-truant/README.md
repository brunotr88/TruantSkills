# Remotion Best Practices - Skill per Claude Code

Una skill completa per [Claude Code](https://docs.anthropic.com/en/docs/claude-code) con **37 regole specializzate** per [Remotion](https://remotion.dev) - il framework per creare video con React.

A comprehensive Claude Code skill with **37 specialized rules** for [Remotion](https://remotion.dev) - the framework for creating videos programmatically in React.

---

## Cosa fa questa skill?

Quando la attivi, Claude Code diventa un esperto di Remotion. Sa tutto su:

- **Safe zone per Instagram Reels** - i margini obbligatori per il formato 9:16, così testo e loghi non vengono coperti dai pulsanti di Instagram
- **Dimensioni font per social media** - le dimensioni minime leggibili per post (1080x810) e reel (1080x1920)
- **Verifica testi italiani** - controllo automatico degli accenti (è, à, ù, ì, ò) e degli apostrofi nei testi
- **37 regole** che coprono animazioni, audio, video, sottotitoli, transizioni, 3D, grafici, mappe e molto altro
- **3 componenti di esempio** pronti all'uso (grafico a barre, effetto macchina da scrivere, evidenziazione parole)

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

## Installazione passo-passo

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

3. **Fatto!** La skill si attiverà automaticamente quando lavori su un progetto Remotion.

### Creare un nuovo progetto Remotion (se non ne hai uno)

```bash
# Con npm
npx create-video@latest il-mio-video

# Con bun (più veloce)
bunx create-video@latest il-mio-video

# Entra nella cartella e avvia
cd il-mio-video
npm start
```

Si aprirà il browser con lo studio di Remotion dove puoi vedere l'anteprima dei tuoi video in tempo reale.

## Come usarla

Una volta installata, la skill si attiva da sola quando Claude Code rileva codice Remotion. Puoi anche invocarla direttamente con questi prompt di esempio:

### Prompt di esempio

```
Crea un Reel Instagram 9:16 con testo animato che rispetti le safe zone

Costruisci un grafico a barre animato con effetto spring

Aggiungi sottotitoli stile TikTok con evidenziazione della parola corrente

Crea un'animazione mappa che mostra il percorso da Roma a Milano con Mapbox

Aggiungi un effetto macchina da scrivere con cursore lampeggiante

Genera barre di visualizzazione audio che reagiscono alla musica

Crea una sequenza di transizioni con fade e light leak
```

## Struttura dei file

```
remotion-skill-powered-by-truant/
├── README.md              # Questo file
├── SKILL.md               # Entry point della skill (caricato da Claude Code)
└── rules/
    ├── 3d.md              # Three.js e React Three Fiber
    ├── animations.md      # Pattern fondamentali di animazione
    ├── assets.md          # Import di immagini, video, audio, font
    ├── audio.md           # Audio: trim, volume, velocità, pitch, loop
    ├── audio-visualization.md  # Barre spettro, waveform, effetti bass
    ├── calculate-metadata.md   # Durata e dimensioni dinamiche
    ├── can-decode.md      # Validazione decodifica video
    ├── charts.md          # Grafici: barre, torta, linee, azioni
    ├── compositions.md    # Composizioni, still, cartelle, props
    ├── display-captions.md     # Visualizzazione sottotitoli TikTok
    ├── extract-frames.md  # Estrazione frame da video
    ├── ffmpeg.md          # Operazioni FFmpeg/FFprobe
    ├── fonts.md           # Google Fonts e font locali
    ├── get-audio-duration.md   # Durata audio
    ├── get-video-dimensions.md # Dimensioni video
    ├── get-video-duration.md   # Durata video
    ├── gifs.md            # GIF, APNG, AVIF, WebP animate
    ├── images.md          # Immagini con <Img>
    ├── import-srt-captions.md  # Import sottotitoli SRT
    ├── light-leaks.md     # Effetti luce WebGL
    ├── lottie.md          # Animazioni Lottie
    ├── maps.md            # Animazioni mappa con Mapbox
    ├── measuring-dom-nodes.md  # Misura elementi DOM
    ├── measuring-text.md  # Misura e adattamento testo
    ├── parameters.md      # Parametri Zod
    ├── sequencing.md      # Pattern Sequence e Series
    ├── sfx.md             # Effetti sonori
    ├── subtitles.md       # Sistema sottotitoli/captions
    ├── tailwind.md        # TailwindCSS in Remotion
    ├── text-animations.md # Macchina da scrivere, highlight
    ├── timing.md          # Interpolazione, spring, easing
    ├── transcribe-captions.md  # Trascrizione con Whisper
    ├── transitions.md     # TransitionSeries, overlay
    ├── transparent-videos.md   # Video trasparenti (ProRes/WebM)
    ├── trimming.md        # Taglio inizio/fine animazioni
    ├── videos.md          # Video: trim, volume, velocità, loop
    ├── voiceover.md       # Voiceover con ElevenLabs TTS
    └── assets/
        ├── charts-bar-chart.tsx            # Componente grafico a barre
        ├── text-animations-typewriter.tsx   # Effetto macchina da scrivere
        └── text-animations-word-highlight.tsx  # Effetto evidenziazione parole
```

## License

[MIT](../LICENSE) - Usa, modifica e condividi liberamente.

---

*Skill creata da [Bruno Truant](https://isipc.com) - Parte della collezione [TruantSkills](https://github.com/brunotr88/TruantSkills).*
