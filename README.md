# Skill per agenti di sviluppo software

Raccolta personale di workflow riutilizzabili per agenti AI che lavorano su
progetti software. Il catalogo segue la
[specifica aperta Agent Skills](https://agentskills.io/specification) ed è
installabile tramite il [CLI `skills`](https://github.com/vercel-labs/skills).

## Iniziare subito

Il comando `skills add` riceve come argomento la sorgente da cui scoprire e
installare le skill. La sorgente può essere un repository GitHub, un URL Git o
una cartella locale.

La sorgente GitHub di questo catalogo è `tosdan/skills`.

### Esplorare il catalogo

Per vedere le skill disponibili senza installare nulla:

```sh
npx skills@latest add tosdan/skills --list
```

### Installazione interattiva

Per avviare il flusso guidato:

```sh
npx skills@latest add tosdan/skills
```

Il CLI analizza il repository, mostra le skill disponibili e permette di
scegliere quali installare. In base agli agenti rilevati può inoltre chiedere le
destinazioni e il metodo di installazione. Senza `--global`, l'installazione è
associata al progetto corrente.

### Installare una skill specifica

Per evitare la selezione della skill:

```sh
npx skills@latest add tosdan/skills --skill pair-program-in-checkpoints
```

Per installare tutte le skill del catalogo:

```sh
npx skills@latest add tosdan/skills --skill '*'
```

### Scegliere agente e ambito

`--agent` indica l'agente di destinazione. `--global` rende la skill disponibile
a livello utente, anziché soltanto nel progetto corrente.

```sh
npx skills@latest add tosdan/skills --skill plan-software-decisions --agent codex --global
```

Altri identificativi supportati includono, per esempio, `claude-code`, `cursor`
e `opencode`.

### Installazione non interattiva

`--yes` accetta automaticamente le conferme. È utile negli script e nei flussi
in cui skill, agente e ambito sono già stati scelti esplicitamente:

```sh
npx skills@latest add tosdan/skills --skill plan-software-decisions --agent codex --global --yes
```

### Usare un checkout locale

Dalla radice di questo repository, usare `.` come sorgente:

```sh
# Elenca le skill locali senza installarle
npx skills@latest add . --list

# Avvia l'installazione interattiva dal catalogo locale
npx skills@latest add .
```

## Catalogo

### `plan-software-decisions`

Da usare per lavori complessi o incerti che richiedono decisioni persistenti
prima dell'implementazione. La skill esamina il repository, crea o riprende un
piano canonico, affronta una decisione alla volta e deriva gli scenari di
accettazione prima di modificare il codice.

```text
Usa $plan-software-decisions per analizzare questa migrazione, creare un piano
persistente e guidarmi attraverso una decisione alla volta.
```

### `pair-program-in-checkpoints`

Da usare per implementare in modo incrementale attraverso checkpoint piccoli e
revisionabili. La skill propone un checkpoint, attende l'approvazione, implementa
soltanto quell'ambito, lo verifica e propone il passo successivo.

```text
Usa $pair-program-in-checkpoints per tradurre questo piano in codice, procedendo
attraverso un checkpoint approvato alla volta.
```

### Usare entrambe le skill

Le skill coprono due fasi consecutive, senza dipendere l'una dall'altra:

1. Usare `plan-software-decisions` mentre restano da chiarire comportamenti o
   decisioni architetturali importanti.
2. Usare `pair-program-in-checkpoints` quando le decisioni e gli scenari di
   accettazione rilevanti sono abbastanza stabili da essere implementati.

È possibile installare e usare ogni skill indipendentemente.

## Struttura del repository

```text
skills/
  <nome-skill>/
    SKILL.md
    agents/        # metadati opzionali per gli agenti
    scripts/       # strumenti eseguibili opzionali
    references/    # documentazione opzionale caricata quando serve
    assets/        # template e risorse statiche opzionali
```

Ogni skill è autosufficiente. Il nome della cartella e il campo `name` del suo
`SKILL.md` devono coincidere e usare il formato kebab-case minuscolo.

## Aggiungere una skill

Creare o spostare ogni skill in `skills/<nome-skill>/`. Il contenuto minimo è:

```markdown
---
name: nome-skill
description: Descrivere cosa fa la skill e in quali situazioni deve essere usata.
---

# Nome della skill

Istruzioni per l'agente.
```

Spostare il materiale dettagliato fuori da `SKILL.md` e collegarlo tramite
percorsi relativi alla cartella della skill. Le istruzioni di installazione e
utilizzo del catalogo appartengono a questo README; le istruzioni operative per
l'agente appartengono al rispettivo `SKILL.md`.

Prima di creare un commit, verificare che il CLI scopra tutte e sole le skill
previste:

```sh
npx skills@latest add . --list
```