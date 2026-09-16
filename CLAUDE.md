# CLAUDE.md — company-to-landing

Repo di una skill per agenti (Claude Code / Codex / Claude app), non un'applicazione: niente build, dipendenze, lint o test automatici.

## Struttura

- `SKILL.md` — frontmatter (`name`, `description`) + workflow in 6 passi (0 intake, 1 ricerca sito, 1b Instagram, 2 brand, 3 checkpoint creativo, 4 design e sviluppo, 5 verifica e consegna). È l'unico `SKILL.md` ammesso nel repo.
- `references/` — caricati dall'agente solo quando servono:
  - `extraction.md` — estrazione di contenuti, brand e media dal sito (economy / Firecrawl).
  - `instagram.md` — handle, verifica identità, strade (export, API, Apify, browser solo riferimento), diritti, elaborazione media.
  - `skill-chain.md` — quale skill installata gestisce ogni fase, file ponte (`.agents/brand-context.md`, `PRODUCT.md`, `DESIGN.md`), regole di riserva.
  - `artifacts.md` — contratti dei file prodotti (`company.json`, `media-manifest.json`, `instagram.json`, `BRAND.md`, `creative-directions.md`, `QA.md`).
  - `providers.md` — provider e costi (snapshot datato: riverificare i prezzi).
- `agents/openai.yaml` — metadati di interfaccia per Codex.
- `README.md`, `CLAUDE.md` — solo per il repo; esclusi dallo zip via `.gitattributes`.

## Convenzioni

- Testo della skill in inglese; esempi di invocazione in italiano.
- `SKILL.md` sotto le 500 righe: i dettagli vanno in `references/` con un link esplicito da `SKILL.md`.
- Link tra file relativi (`references/x.md` da `SKILL.md`, `x.md` tra i reference). Quando aggiungi, rinomini o elimini un reference, aggiorna i link e la sezione Struttura qui sopra nello stesso commit.
- `description` nel frontmatter: massimo 1024 caratteri, niente `<` o `>`. È il meccanismo di attivazione della skill: modificarla cambia quando la skill scatta.
- Mai inserire token, chiavi o URL con `access_token` negli esempi.
- File con fine riga LF (`.gitattributes`): il parser del frontmatter richiede `---\n`.

## Verifica dopo una modifica

Validatore di skill-creator (richiede PyYAML; su Windows serve `PYTHONUTF8=1`), da lanciare dalla cartella della skill skill-creator:

```bash
PYTHONUTF8=1 python -m scripts.quick_validate <percorso-di-questo-repo>
```

Controlla poi che ogni link `](references/...)` / `](*.md)` punti a un file esistente.

## Copie installate

Le macchine del team installano la skill clonando questo repo in `~/.claude/skills/company-to-landing` e/o `~/.codex/skills/company-to-landing` (vedi README). Dopo il push, le copie si aggiornano con `git pull`; le copie non clonate vanno sostituite a mano.
