---
name: plan-software-decisions
description: Guide complex software work through a persistent, decision-first planning process before implementation. Use when a project has many uncertain tasks, needs stabilization, redesign, migration or architectural clarification, or when the user asks to create a durable plan, compare alternatives, proceed one decision at a time, maintain a granular checklist, or resume from one explicit next step.
---

# Plan Software Decisions

Guidare il progetto attraverso decisioni esplicite, verificabili e persistenti prima dell'implementazione.

## Regole fondamentali

- Ispezionare le evidenze reali del repository prima di proporre cambiamenti.
- Distinguere fatti verificati, ipotesi, rischi e decisioni aperte.
- Creare o aggiornare un piano Markdown canonico e versionabile.
- Discutere una sola decisione indipendente alla volta.
- Formulare una raccomandazione motivata, non soltanto elencare opzioni.
- Registrare ogni decisione immediatamente dopo l'approvazione.
- Mantenere un solo `Prossimo passo`, preciso e operativo.
- Non modificare il comportamento applicativo prima dell'approvazione delle decisioni e degli scenari necessari.
- Segnalare immediatamente contraddizioni con decisioni precedenti.
- Rispettare gli aspetti dichiarati fuori scope.

## Avviare il lavoro

1. Leggere eventuali istruzioni del repository.
2. Ispezionare codice, documentazione, test, configurazione e stato Git rilevanti.
3. Non modificare ancora il comportamento applicativo.
4. Identificare:
   - comportamento implementato e verificato;
   - comportamento implementato ma non verificato;
   - lavoro incompleto;
   - rischi e ambiguita;
   - decisioni necessarie.
5. Cercare un piano canonico esistente.
6. Se manca, usare `assets/work-plan-template.md` come base e salvarlo in una posizione coerente, di default `docs/work-plan.md`.
7. Impostare la prima decisione irrisolta come `Prossimo passo`.
8. Sottoporre soltanto quella decisione all'utente.

La creazione e l'aggiornamento di piano, registro decisionale e glossario sono autorizzate dal workflow. Richiedere autorizzazione esplicita prima di passare a test che cambiano il progetto o all'implementazione.

## Mantenere il piano canonico

Includere sempre:

- stato complessivo;
- fase corrente;
- un solo prossimo passo;
- obiettivo;
- ambito incluso ed escluso;
- situazione iniziale verificata;
- definizione di completamento;
- decisioni numerate;
- checklist granulari;
- scenari di accettazione;
- registro delle decisioni;
- fasi tecniche e di verifica;
- diario di avanzamento.

Non marcare un'attivita come completata senza evidenza.

Quando un piano esiste gia:

1. Leggerlo prima di progettare.
2. Verificare rapidamente che il repository non lo abbia reso obsoleto.
3. Riassumere brevemente le decisioni approvate.
4. Riprendere dal `Prossimo passo`.
5. Non ricominciare la progettazione da zero.

## Condurre il ciclo decisionale

Per ogni decisione presentare:

1. identificativo e titolo;
2. problema concreto;
3. scenario che renda visibile il problema;
4. comportamento attuale o evidenza disponibile;
5. alternative realistiche;
6. vantaggi, svantaggi e conseguenze;
7. alternativa raccomandata;
8. motivazione specifica per il progetto;
9. una sola domanda di approvazione.

Non presentare insieme decisioni indipendenti. Non inventare alternative deboli per favorire artificiosamente la raccomandazione.

Valutare le alternative rispetto a:

- obiettivo principale;
- correttezza;
- recuperabilita;
- idempotenza;
- osservabilita;
- semplicita concettuale;
- complessita implementativa e operativa;
- casi limite;
- architettura esistente;
- rischio di perdita dati o effetti duplicati.

## Registrare la risposta dell'utente

Dopo ogni risposta:

1. aggiornare immediatamente il piano;
2. registrare data, decisione, motivazione e conseguenze;
3. aggiungere scenari di accettazione concreti;
4. aggiornare le checklist;
5. aggiornare il diario;
6. impostare il prossimo elemento irrisolto come `Prossimo passo`;
7. solo allora presentare la decisione successiva.

Se l'utente modifica la raccomandazione, registrare fedelmente la scelta effettiva.

Se emerge un nuovo tema:

- aggiungerlo subito alla coda delle decisioni;
- indicare dove verra affrontato;
- non interrompere il quesito corrente se il nuovo tema non lo blocca.

Suddividere decisioni complesse in sottodecisioni come `D04.1`, `D04.2` e `D04.3`. Non chiudere la decisione principale prima di risolvere tutti i compromessi necessari.

## Gestire linguaggio e contraddizioni

Quando un termine importante e ambiguo:

- proporre un nome canonico;
- distinguerlo dai concetti vicini;
- confrontarlo con codice e decisioni precedenti;
- registrare la definizione in un glossario, se utile.

Mantenere il glossario privo di dettagli implementativi.

Quando una richiesta contraddice una decisione approvata:

1. indicare la decisione in conflitto;
2. spiegare la conseguenza concreta;
3. chiedere se revisionarla;
4. aggiornare tutte le sezioni coinvolte se viene modificata.

Non lasciare regole contraddittorie nel piano o nel glossario.

## Derivare scenari di accettazione

Scrivere ogni scenario nella forma:

> Dato [stato iniziale], quando [evento], allora [risultato osservabile ed effetti consentiti o vietati].

Considerare quando pertinenti:

- successo;
- errore transitorio;
- errore deterministico;
- esaurimento retry;
- input duplicati;
- concorrenza;
- eventi fuori ordine;
- riavvio e recupero;
- stato persistito incoerente;
- dry-run o simulazione.

Non progettare test basati su ipotesi non approvate.

## Valutare la soluzione tecnica dopo il comportamento

Decidere prima la semantica funzionale e poi framework e infrastruttura.

Quando i requisiti includono state machine, code, retry, scheduling, locking, esecuzione durevole o orchestrazione:

1. aggiungere una decisione tecnica esplicita;
2. ricercare soluzioni esistenti mantenute usando fonti primarie;
3. confrontarle con una soluzione locale minima;
4. valutare compatibilita, persistenza, recupero, garanzie atomiche, dipendenze infrastrutturali, testabilita, costo operativo, manutenzione e migrazione;
5. formulare una raccomandazione;
6. ottenere approvazione prima di implementare.

Non reinventare infrastruttura senza questa valutazione.

## Controllare lo scope

Non espandere il lavoro verso deploy, sicurezza, UI, refactoring o packaging se non sono necessari all'obiettivo corrente.

Quando emerge un tema secondario importante:

1. registrarlo;
2. spiegarne brevemente la rilevanza;
3. lasciarlo in attesa fino al suo turno.

## Passare all'implementazione

Iniziare soltanto quando:

- le decisioni richieste sono approvate;
- gli scenari di accettazione sono registrati;
- la soluzione tecnica e approvata;
- l'utente autorizza esplicitamente l'implementazione.

Prima di modificare il codice:

1. convertire gli scenari approvati in checklist di test;
2. identificare test di caratterizzazione del comportamento corrente;
3. identificare i test che devono fallire prima delle correzioni;
4. mantenere le modifiche localizzate quando possibile.

Durante l'implementazione aggiornare il piano dopo ogni incremento verificato e mantenere accurato il `Prossimo passo`.

## Completare il lavoro

Considerare concluso il lavoro soltanto quando:

- le decisioni sono registrate;
- gli scenari di accettazione passano;
- l'implementazione e verificata;
- la validazione controllata e conclusa quando richiesta;
- la documentazione corrisponde al comportamento;
- non restano checklist obbligatorie aperte;
- il piano indica `Completato` oppure un unico prossimo passo residuo.
