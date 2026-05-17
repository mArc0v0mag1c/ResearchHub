## LaTeX assets

Personal LaTeX style files. Versioned here so new machines can re-create the local TeX tree without losing customizations.

### `marcoreport.sty`

Personal report style — margins, theorem environments, `remarkbox`, math shortcuts (`\RR`, `\EE`, `\vct`, `\mat`, `\var`), tikz/tcolorbox setup. Loaded via `\usepackage{marcoreport}` from any `.tex` that wants the shared formatting.

### Install on a new Mac (TinyTeX)

```bash
mkdir -p ~/Library/TinyTeX/texmf-local/tex/latex/marco
ln -s ~/vscodeproject/ResearchHub/latex/marcoreport.sty \
      ~/Library/TinyTeX/texmf-local/tex/latex/marco/marcoreport.sty
tlmgr conf texmf-local "$HOME/Library/TinyTeX/texmf-local"  # usually pre-configured
mktexlsr ~/Library/TinyTeX/texmf-local
```

### Install on Windows (MiKTeX)

```cmd
mkdir "%APPDATA%\MiKTeX\tex\latex\marcoreport"
copy marcoreport.sty "%APPDATA%\MiKTeX\tex\latex\marcoreport\"
initexmf --update-fndb
```

Symlinking on Windows works too but requires admin or Developer Mode. Plain `copy` is simpler.

### Editing

Edit the copy here. After editing, run `mktexlsr` only if you renamed or added files — content changes don't need a refresh.
