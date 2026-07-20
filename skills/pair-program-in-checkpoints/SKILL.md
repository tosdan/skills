---
name: pair-program-in-checkpoints
description: Guida lo sviluppo di un software in modalità pair programming incrementale attraverso checkpoint piccoli, concordati e verificabili. Usare quando l'utente chiede di tradurre piani, specifiche, mockup, user flow o documenti in codice procedendo passo passo; vuole calibrare insieme i primi esempi prima di lavorare in batch; chiede approvazione tra uno step e il successivo; oppure vuole evitare modifiche ampie, assunzioni implicite e refactoring opportunistici.
---

# Pair programming a checkpoint

## Impostare il lavoro

1. Leggere le istruzioni del repository, il materiale indicato, il codice coinvolto, i test e lo stato corrente del worktree.
2. Separare i fatti osservati da requisiti espliciti, ipotesi, decisioni già prese e dipendenze esterne ancora ignote.
3. Inizializzare o riprendere il registro e gestire gli eventuali documenti preesistenti secondo la sezione "Registrare il lavoro della skill".
4. Concordare la granularità, salvo che sia già registrata per il lavoro o che l'utente l'abbia indicata chiaramente.
5. Individuare il checkpoint più piccolo compatibile con la granularità scelta che riduca un'incertezza o produca un risultato revisionabile.
6. Registrarlo come unico prossimo checkpoint, proporlo con una motivazione breve e attendere l'approvazione prima di eseguirlo.

Se l'utente ha già approvato un checkpoint concreto, completare comunque l'impostazione e la registrazione iniziali, poi eseguirlo senza chiedere una seconda conferma sul checkpoint.

## Registrare il lavoro della skill

Identificare un nome breve e stabile per ogni lavoro avviato con questa skill. Creare il relativo registro da `assets/checkpoint-plan-template.md`, sotto un percorso inequivocabilmente dedicato a `pair-program-in-checkpoints` e di default in `docs/pair-program-in-checkpoints/<nome-lavoro>.md`.

Creare e mantenere il registro anche quando il lavoro è breve, prevede un solo checkpoint o si conclude nella sessione corrente. Non usare un piano o un documento preesistente dell'utente come sostituto.

Quando si riprende lo stesso lavoro, riutilizzare il registro esistente invece di crearne uno concorrente. Verificare che corrisponda allo stato reale del repository prima di proseguire.

Se durante l'impostazione vengono trovati documenti preesistenti pertinenti:

1. elencarli in modo conciso;
2. chiedere esplicitamente se l'utente vuole mantenerli sincronizzati;
3. ricordare che avanzamento e checkpoint saranno registrati comunque nel file specifico della skill;
4. registrare nel file della skill la scelta e i documenti autorizzati;
5. non modificare i documenti esterni se l'utente non ha dato il consenso.

Chiedere questa preferenza una sola volta per il lavoro. Nelle sessioni successive riutilizzare la scelta registrata, salvo una richiesta esplicita dell'utente.

## Concordare la granularità

All'inizio del lavoro proporre queste modalità:

- **Esplorativa**: separare analisi, decisione, test e implementazione in checkpoint distinti. Usarla per codice sconosciuto, rischioso o ancora ambiguo.
- **Bilanciata (consigliata)**: completare un solo piccolo comportamento osservabile per checkpoint. Includere tutto ciò che serve per renderlo funzionante e verificato, ma nessun comportamento appartenente al checkpoint successivo.
- **Ripetitiva controllata**: applicare a pochi casi equivalenti un pattern già approvato. Usarla soltanto dopo aver revisionato almeno un esempio e senza introdurre nuove decisioni.

Chiedere all'utente di scegliere una modalità una sola volta, all'inizio del lavoro, e attendere la risposta. Se delega esplicitamente la scelta, adottare la modalità Bilanciata. Registrare la modalità nel registro della skill e riutilizzarla nei checkpoint e nelle sessioni successive senza ripetere la domanda.

Non proporre di cambiare modalità durante il lavoro. Modificarla soltanto quando l'utente lo richiede esplicitamente. Se un checkpoint cresce o non rispetta più i limiti, suddividerlo mantenendo la modalità corrente.

Applicare sempre questi limiti, indipendentemente dalla modalità:

- perseguire un solo obiettivo concettuale;
- dichiarare prima dell'esecuzione le aree o i file attesi, la verifica prevista e una stima della dimensione;
- non combinare nello stesso checkpoint contratto, state, UI, styling e refactoring quando possono essere revisionati separatamente;
- dividere il checkpoint se si prevedono più di circa 100 righe modificate manualmente, oppure ottenere un'approvazione specifica motivata;
- escludere dal limite numerico file generati, lockfile e snapshot, ma segnalarli nella stima;
- fermarsi e proporre una suddivisione se durante l'esecuzione emergono nuove decisioni o lo scope cresce.

Usare il conteggio delle righe solo come segnale di allarme. La misura principale resta la presenza di un solo risultato revisionabile.

## Esempi di checkpoint

Preferire risultati come:

- chiarire una regola di dominio;
- aggiungere un modello o un contratto;
- coprire un comportamento con un test;
- implementare una sola trasformazione completa e verificabile;
- collegare un comportamento già verificato al template;
- riallineare un documento ormai obsoleto;
- eseguire una verifica di regressione.

Non anticipare i checkpoint successivi.

## Usare il termine seam

Un **seam** è un punto in cui è possibile modificare il comportamento senza intervenire direttamente in quel punto; è il luogo in cui vive l'interfaccia di un modulo. Decidere dove collocare il seam è una scelta di design distinta da ciò che viene collocato dietro di esso.

Usare `seam` con questo significato quando si identifica l'interfaccia pubblica attraversata da chiamanti e test. Non usarlo come sinonimo generico di file, classe, livello o confine.

Definizione adattata dalla skill [`codebase-design`](https://github.com/mattpocock/skills/tree/main/skills/engineering/codebase-design) di Matt Pocock, basata sulla terminologia di Michael Feathers.

## Eseguire il checkpoint

1. Verificare nuovamente i file interessati prima di modificarli, soprattutto dopo interruzioni o riavvii.
2. Dichiarare in modo conciso il seam, l'assunzione o il risultato perseguito.
3. Applicare esclusivamente le modifiche necessarie al checkpoint concordato.
4. Conservare le modifiche dell'utente e ignorare il lavoro non correlato.
5. Eseguire prima la verifica mirata, poi controlli più ampi proporzionati al rischio.
6. Aggiornare il registro della skill e gli eventuali documenti autorizzati secondo la sezione "Mantenere la pianificazione viva".
7. Fermarsi dopo il checkpoint e proporre un solo passo successivo.

Quando l'utente dice «procedi» o una formula equivalente, interpretarla come approvazione dell'ultimo checkpoint proposto, non come autorizzazione a completare in batch l'intero piano.

## Gestire requisiti e incertezze

- Non inventare regole di dominio, limitazioni o comportamenti UX non specificati.
- Non trasformare una possibilità in un requisito senza evidenza nei materiali o nel codice di riferimento.
- Lasciare al backend le decisioni che gli appartengono quando il frontend deve soltanto inoltrare dati e rappresentare l'esito.
- Chiedere una decisione soltanto quando alternative plausibili produrrebbero risultati materialmente diversi e il contesto locale non permette di scegliere.
- Se emerge che una decisione precedente poggiava su un presupposto errato, correggere prima modello mentale, registro della skill ed eventuali documenti autorizzati. Non costruire altro lavoro sopra l'errore.
- Distinguere sempre comportamento funzionale, contratto backend, aggiornamento dello state, feedback UI, styling e refactoring.

## Testare attraverso seam pubblici

Quando si introduce un comportamento nuovo:

1. Concordare o rendere esplicito il seam pubblico da osservare.
2. Scrivere un test comportamentale prima dell'implementazione quando il progetto e il checkpoint lo consentono.
3. Eseguire la fase rossa e implementare soltanto quanto serve per arrivare al verde.
4. Se il comportamento esiste già, trattare il test come caratterizzazione: accettare che sia subito verde e non produrre un fallimento artificiale.
5. Evitare metodi privati, dettagli meccanici e mock di collaboratori interni quando è possibile attraversare il modulo reale e sostituire soltanto una dipendenza al seam esterno.
6. Usare il linguaggio del dominio e la lingua stabilita dal progetto nei nomi dei test.
7. Non dichiarare coperto un ramo più ampio di quello effettivamente verificato.

## Proteggere modifiche sensibili

- Non introdurre refactoring opportunistici durante un checkpoint funzionale.
- Per modifiche visuali, stilistiche, distruttive o difficili da annullare, descrivere l'effetto puntuale e ottenere conferma specifica.
- Preparare una variante reversibile o un confronto A/B quando una modifica visuale può perdere lavoro già valido.
- Ricavare convenzioni da esempi reali del repository o del progetto di riferimento prima di creare nuove astrazioni.

## Mantenere la pianificazione viva

Usare il registro specifico della skill come fonte canonica per l'avanzamento dei checkpoint. Aggiornarlo dopo ogni checkpoint, indipendentemente dalla durata del lavoro o dal numero di sessioni, almeno con risultato, stato, verifiche, decisioni emerse e unico prossimo checkpoint.

Trattare eventuali piani o documenti preesistenti come destinazioni secondarie e opzionali. Aggiornarli soltanto se l'utente li ha autorizzati durante l'impostazione; non duplicare indiscriminatamente il registro e non usarli al posto del file della skill.

Usare stati espliciti:

- **Completato**: comportamento implementato e verificato;
- **Parziale**: solo una parte precisa è stata completata;
- **Differito**: manca un contratto o una decisione esterna;
- **Non necessario**: il requisito non si applica allo scenario corrente;
- **Aperto e separato**: attività valida ma non bloccante per il risultato corrente.

Registrare anche le decisioni deliberate di non implementare qualcosa e la ragione che le rende corrette nel contesto attuale. Non segnare un'attività come completata senza indicare l'evidenza di verifica.

## Chiudere ogni checkpoint

Restituire un riepilogo autosufficiente e breve con:

- risultato ottenuto;
- file o aree modificati;
- verifiche eseguite e relativo esito;
- aggiornamento apportato al registro della skill;
- eventuali documenti esterni sincronizzati;
- limiti ancora presenti;
- un solo checkpoint successivo consigliato.

Attendere quindi la conferma dell'utente. Passare a un intervento batch soltanto dopo un'autorizzazione esplicita, quando i primi esempi hanno stabilizzato regole e convenzioni.
