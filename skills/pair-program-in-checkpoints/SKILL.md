---
name: pair-program-in-checkpoints
description: Guida il lavoro software in modalità pair programming incrementale attraverso checkpoint piccoli, concordati e verificabili. Usare quando l'utente chiede di tradurre piani, specifiche, mockup, user flow o documenti in codice procedendo passo passo; vuole calibrare insieme i primi esempi prima di lavorare in batch; chiede approvazione tra uno step e il successivo; oppure vuole evitare modifiche ampie, assunzioni implicite e refactoring opportunistici.
---

# Pair programming a checkpoint

## Impostare il lavoro

1. Leggere le istruzioni del repository, il materiale indicato, il codice coinvolto, i test e lo stato corrente del worktree.
2. Separare i fatti osservati da requisiti espliciti, ipotesi, decisioni già prese e dipendenze esterne ancora ignote.
3. Individuare il checkpoint più piccolo che riduca un'incertezza o produca un risultato revisionabile.
4. Proporre un solo checkpoint con una motivazione breve e attendere l'approvazione prima di eseguirlo.

Se l'utente ha già approvato un checkpoint concreto, eseguirlo senza chiedere una seconda conferma.

## Dimensionare un checkpoint

Definire un solo risultato concettuale per checkpoint. Preferire, per esempio:

- chiarire una regola di dominio;
- aggiungere un modello o un contratto;
- coprire un comportamento con un test;
- implementare la trasformazione minima necessaria;
- collegare un comportamento già verificato al template;
- riallineare un documento ormai obsoleto;
- eseguire una verifica di regressione.

Non combinare nello stesso checkpoint contratto, state, UI, styling e refactoring se possono essere revisionati separatamente. Non anticipare i checkpoint successivi.

## Eseguire il checkpoint

1. Verificare nuovamente i file interessati prima di modificarli, soprattutto dopo interruzioni o riavvii.
2. Dichiarare in modo conciso il seam, l'assunzione o il risultato perseguito.
3. Applicare esclusivamente le modifiche necessarie al checkpoint concordato.
4. Conservare le modifiche dell'utente e ignorare il lavoro non correlato.
5. Eseguire prima la verifica mirata, poi controlli più ampi proporzionati al rischio.
6. Aggiornare la pianificazione quando il codice rende obsolete analisi o decisioni precedenti.
7. Fermarsi dopo il checkpoint e proporre un solo passo successivo.

Quando l'utente dice «procedi» o una formula equivalente, interpretarla come approvazione dell'ultimo checkpoint proposto, non come autorizzazione a completare in batch l'intero piano.

## Gestire requisiti e incertezze

- Non inventare regole di dominio, limitazioni o comportamenti UX non specificati.
- Non trasformare una possibilità in un requisito senza evidenza nei materiali o nel codice di riferimento.
- Lasciare al backend le decisioni che gli appartengono quando il frontend deve soltanto inoltrare dati e rappresentare l'esito.
- Chiedere una decisione soltanto quando alternative plausibili produrrebbero risultati materialmente diversi e il contesto locale non permette di scegliere.
- Se emerge che una decisione precedente poggiava su un presupposto errato, correggere prima modello mentale, documentazione e piano. Non costruire altro lavoro sopra l'errore.
- Distinguere sempre comportamento funzionale, contratto backend, aggiornamento dello state, feedback UI, styling e refactoring.

## Testare attraverso seam pubblici

Quando si introduce un comportamento nuovo:

1. Concordare o rendere esplicito il seam pubblico da osservare.
2. Scrivere un test comportamentale prima dell'implementazione quando il progetto e il checkpoint lo consentono.
3. Eseguire la fase rossa e implementare soltanto quanto serve per arrivare al verde.
4. Se il comportamento esiste già, trattare il test come caratterizzazione: accettare che sia subito verde e non produrre un fallimento artificiale.
5. Evitare metodi privati, dettagli meccanici e mock di collaboratori interni quando è possibile attraversare il modulo reale e sostituire soltanto un confine esterno.
6. Usare il linguaggio del dominio e la lingua stabilita dal progetto nei nomi dei test.
7. Non dichiarare coperto un ramo più ampio di quello effettivamente verificato.

## Proteggere modifiche sensibili

- Non introdurre refactoring opportunistici durante un checkpoint funzionale.
- Per modifiche visuali, stilistiche, distruttive o difficili da annullare, descrivere l'effetto puntuale e ottenere conferma specifica.
- Preparare una variante reversibile o un confronto A/B quando una modifica visuale può perdere lavoro già valido.
- Ricavare convenzioni da esempi reali del repository o del progetto di riferimento prima di creare nuove astrazioni.

## Mantenere la pianificazione viva

Aggiornare i documenti con stati espliciti:

- **Completato**: comportamento implementato e verificato;
- **Parziale**: solo una parte precisa è stata completata;
- **Differito**: manca un contratto o una decisione esterna;
- **Non necessario**: il requisito non si applica allo scenario corrente;
- **Aperto e separato**: attività valida ma non bloccante per il risultato corrente.

Registrare anche le decisioni deliberate di non implementare qualcosa e la ragione che le rende corrette nel contesto attuale.

## Chiudere ogni checkpoint

Restituire un riepilogo autosufficiente e breve con:

- risultato ottenuto;
- file o aree modificati;
- verifiche eseguite e relativo esito;
- limiti ancora presenti;
- un solo checkpoint successivo consigliato.

Attendere quindi la conferma dell'utente. Passare a un intervento batch soltanto dopo un'autorizzazione esplicita, quando i primi esempi hanno stabilizzato regole e convenzioni.
