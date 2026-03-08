# Prompt di installazione - Remotion + TruantSkills

Copia e incolla il prompt qui sotto direttamente in Claude Code.
Claude si occuperà di tutto: installare la skill, creare il progetto, aggiungere tutti i pacchetti.

---

## Prompt da copiare

```
Utilizza sequential-thinking per pianificare ed eseguire questa installazione in modo ordinato.
Crea un team di agenti dedicato per parallelizzare le operazioni dove possibile.

Esegui queste operazioni in sequenza. Non chiedere conferma, procedi automaticamente.

### STEP 1: Installa la skill TruantSkills per Remotion

Clona il repository e copia la skill nella directory corretta:

git clone https://github.com/brunotr88/TruantSkills.git /tmp/TruantSkills
mkdir -p ~/.agents/skills
cp -r /tmp/TruantSkills/remotion-skill-powered-by-truant ~/.agents/skills/remotion-best-practices
rm -rf /tmp/TruantSkills

Verifica che la skill sia stata installata controllando che esista il file ~/.agents/skills/remotion-best-practices/SKILL.md

### STEP 2: Crea la cartella progetti e il progetto Remotion

Crea la cartella C:\PROGETTI se non esiste già, poi crea dentro una sottocartella dedicata a Remotion:

mkdir -p /mnt/c/PROGETTI/remotion
cd /mnt/c/PROGETTI/remotion
npx create-video@latest remotion-studio
cd remotion-studio

### STEP 3: Installa TUTTI i pacchetti Remotion

Installa l'ecosistema completo di pacchetti Remotion. Usa il package manager già presente nel progetto (controlla se esiste bun.lock, package-lock.json, yarn.lock o pnpm-lock.yaml).

Ecco la lista completa. Usa "npx remotion add" per i pacchetti @remotion/* (garantisce compatibilità versioni):

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

### STEP 4: Verifica installazione

1. Controlla che tutti i pacchetti siano nel package.json
2. Avvia lo studio Remotion con "npm run dev" per verificare che tutto funzioni
3. Conferma che la skill è attiva mostrando il contenuto di ~/.agents/skills/remotion-best-practices/SKILL.md

### STEP 5: Riepilogo

Mostra un riepilogo finale di cosa è stato installato:
- Numero pacchetti Remotion installati
- Path della skill
- Comando per avviare lo studio: npm run dev (apre il browser con anteprima live)
- Comando per esportare un video: npx remotion render <CompositionId> output.mp4
- Comando per aggiornare Remotion: npx remotion upgrade
```

---

## Come usare questo prompt

1. Apri un terminale (WSL su Windows, o terminale su Mac/Linux)
2. Avvia Claude Code con `claude`
3. Incolla il prompt qui sopra e premi Invio
4. Claude farà tutto da solo in pochi minuti
5. Il progetto verrà creato in `C:\PROGETTI\remotion\remotion-studio\`

## Note importanti

- **`npx remotion add`** è il modo ufficiale per aggiungere pacchetti Remotion. Gestisce automaticamente la compatibilità delle versioni tra tutti i pacchetti.
- Se usi **bun** invece di npm, sostituisci `npx` con `bunx` in tutti i comandi.
- La skill si attiva **automaticamente** quando Claude Code rileva file `.tsx` che importano da `remotion`.
- Per **aggiornare** Remotion in futuro: `npx remotion upgrade`

## Cosa viene installato - Tabella completa

### Pacchetti Remotion (21 pacchetti)

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

### Pacchetti Third-Party (3 pacchetti)

| Pacchetto | A cosa serve |
|---|---|
| `zod` | Schema validation per rendere i video parametrizzabili |
| `lucide-react` | Icone SVG moderne e leggere |
| `react-icons` | Mega-libreria con migliaia di icone (Font Awesome, Material, ecc.) |

### La Skill (37 regole + 3 componenti)

La skill `remotion-best-practices` insegna a Claude Code tutto quello che serve su Remotion:
- Come animare (useCurrentFrame, spring, interpolate, easing)
- Safe zone per Instagram Reels (dove mettere testo e loghi)
- Dimensioni font per social media
- Verifica automatica accenti e apostrofi nei testi italiani
- Pattern per audio, video, sottotitoli, transizioni, grafici, mappe 3D
- 3 componenti di esempio pronti da copiare
