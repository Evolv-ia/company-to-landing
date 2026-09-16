# company-to-landing

Skill per agenti di coding (Claude Code, Codex, Claude app) che trasforma una descrizione aziendale, un URL e, facoltativamente, un handle Instagram in una landing page dinamica e verificata.

Flusso in breve:

0. **Intake** — descrizione, URL, handle Instagram (chiesto se manca, o trovato sul sito ufficiale).
1. **Ricerca sul sito** — fatti, contatti, media, token del brand, con fonti tracciate.
1b. **Media da Instagram** — verifica che l'account sia dell'azienda, poi foto e video da export ufficiale, cartella, API o Apify (solo con budget approvato), con controllo dei diritti.
2. **Brand** — orchestrata con le skill di branding installate (`brand-positioning`, `brand-voice`, `brand-messaging`, `brand-identity`, …) alimentate con le prove raccolte.
3. **Checkpoint creativo** — 2-3 direzioni creative distinte con raccomandazione; attende la scelta (salvo "modalità autonoma").
4. **Design e sviluppo** — `PRODUCT.md` + `DESIGN.md` generati per `impeccable` (fallback `frontend-design`).
5. **Verifica e consegna** — build, test nel browser, revisione di design, `QA.md`.

Dettagli in [SKILL.md](SKILL.md) e in `references/`.

## Installazione

### Claude Code

Windows (PowerShell):

```powershell
git clone https://github.com/Evolv-ia/company-to-landing.git "$env:USERPROFILE\.claude\skills\company-to-landing"
```

macOS / Linux:

```bash
git clone https://github.com/Evolv-ia/company-to-landing.git ~/.claude/skills/company-to-landing
```

Si usa con `/company-to-landing <URL o descrizione> @handle`, oppure chiedendo una landing per un'azienda: la skill si attiva da sola.

### Codex

Stesso comando, cambiando la destinazione in `~/.codex/skills/company-to-landing` (Windows: `$env:USERPROFILE\.codex\skills\company-to-landing`). Si invoca con `$company-to-landing`.

### Claude app (chat / Cowork)

Genera lo zip dalla cartella clonata e caricalo da Impostazioni → Capabilities → Skills:

```bash
git archive --format=zip --prefix=company-to-landing/ -o company-to-landing.zip HEAD
```

`README.md`, `CLAUDE.md` e i file git sono esclusi dallo zip tramite `.gitattributes`.

### Aggiornare

```bash
git -C ~/.claude/skills/company-to-landing pull
```

## Skill collegate (facoltative)

La skill funziona anche da sola: per ogni fase ha regole di riserva in `references/skill-chain.md`. Il risultato migliora se sono installate:

- brainstorming: `superpowers:brainstorming`
- branding: `brand-context`, `brand-positioning`, `competitor-branding`, `brand-voice`, `brand-messaging`, `brand-identity`, `rebranding`
- design: `impeccable`, `ui-ux-pro-max`, `frontend-design`, `design-shotgun`, `design-review`

## Accesso

Il repo è privato. Per condividerlo aggiungi un collaboratore in sola lettura:

```bash
gh api -X PUT repos/Evolv-ia/company-to-landing/collaborators/<username-github> -f permission=pull
```

## Requisiti

Accesso web, un ambiente di sviluppo e un browser per la verifica visiva. Firecrawl, Apify e la generazione di media sono opzionali e si usano solo entro il budget indicato dall'utente.
