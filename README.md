# Registra Presenze

**Sistema di rilevazione delle presenze dei volontari di Protezione Civile.**

[**Ultima versione**](../../releases/latest) · Windows · funzionamento senza connessione

Registra Presenze è un applicativo per la rilevazione degli ingressi e delle uscite dei volontari
di Protezione Civile nel corso degli eventi. L'identificazione avviene mediante la lettura del
codice fiscale dal codice a barre del **tesserino regionale di Regione Lombardia** o della
**tessera sanitaria**; qualora il volontario ne sia sprovvisto, l'identificazione può essere
effettuata per cognome e nome.

L'elenco dei volontari viene importato dal file Excel dell'evento, che non subisce alcuna
modifica. Al termine dell'evento l'applicativo produce il registro delle presenze compilato con
gli orari di ciascuna giornata, nel rispetto della formattazione del file di origine.
L'applicativo è distribuito come unico file di installazione, non richiede privilegi di
amministratore né registrazione di account e conserva i dati esclusivamente sul computer della
postazione.

## Funzionamento

1. **Caricamento del registro.** Si seleziona il file Excel dei volontari; le colonne sono
   riconosciute automaticamente e la corrispondenza proposta può essere rettificata prima
   dell'importazione.
2. **Lettura delle tessere.** Le letture di una stessa tessera registrano alternativamente
   ingresso e uscita: la prima registra l'ingresso, la seconda l'uscita, le successive gli
   eventuali rientri. Non è richiesta la selezione di alcuna modalità operativa.
3. **Chiusura dell'evento.** Prima della chiusura viene presentato l'elenco dei volontari privi
   di registrazione dell'uscita; successivamente viene generato il registro compilato, predisposto
   per il salvataggio e la stampa.

## Formato dei file Excel

### Elenco dei volontari

Il foglio contiene una riga di intestazione e un volontario per riga. La riga di intestazione può
essere preceduta da un titolo in celle unite, dal quale viene proposta la denominazione
dell'evento.

| N. | ETS | COGNOME | NOME | CF | DATA | TURNO | SQUADRA |
|---|---|---|---|---|---|---|---|
| 1 | PC VALLEVERDE | ROSSI | MARIO | RSSMRA85M01F205Z | 12/09, 13/09 | 08-12, 14-18 | SQ1, SQ2 |
| 2 | PC VALLEVERDE | BIANCHI | LAURA | BNCLRA90A41F205X | 12/09 | 14-18 | SQ2 |
| 3 | RADIO SOCCORSO | VERDI | GIUSEPPE | VRDGPP78C12L219K | 12/09 - 13/09 | Tutto il giorno | SQ1 |
| 4 | PC COLLINA | NERI | ANNA | NRENNA82D50D969P | | | SQ3 |

- Sono indispensabili le colonne `CF`, `COGNOME` e `NOME`; le altre sono facoltative e possono
  comparire in qualsiasi ordine. Sono riconosciute anche intestazioni equivalenti, quali
  `CODICE FISCALE`, `ENTE` o `ASSOCIAZIONE`, `GIORNI` e `FASCIA ORARIA`.
- Turni e squadre sono abbinati alle date nell'ordine indicato: nella riga 1 il volontario è
  atteso il 12/09 nel turno 08-12 con la squadra SQ1, e il 13/09 nel turno 14-18 con la squadra
  SQ2. Un valore unico, come nella riga 3, vale per tutte le giornate.
- Una cella `DATA` vuota, come nella riga 4, indica un volontario atteso in tutte le giornate
  dell'evento, senza turno.
- Le date prive di anno si riferiscono all'anno di caricamento del file.
- Non è necessario predisporre le colonne degli orari, che vengono generate nel registro
  compilato.

### Inventario del materiale

Il foglio contiene una riga di intestazione e un oggetto per riga.

| TIPO | IDENTIFICATIVO |
|---|---|
| RADIO | R01 |
| RADIO | R02 |
| RADIO | R03 |
| BATTERIA | B01 |
| BATTERIA | B02 |

- La colonna `IDENTIFICATIVO` è l'unica indispensabile; sono accettate anche le intestazioni
  `CODICE`, `ID`, `SIGLA`, `MATRICOLA` e `SERIALE`.
- La colonna `TIPO` è facoltativa: ove assente o vuota, si applica il tipo selezionato nella
  sezione **Materiale** al momento del caricamento.
- Gli oggetti già presenti in inventario non vengono modificati, e un identificativo ripetuto
  nel file è considerato una sola volta. Le righe prive di identificativo sono scartate e
  segnalate.

## Funzionalità

### Importazione del registro

L'importazione accetta file Excel in formato `.xlsx` contenenti l'elenco dei volontari. Le
colonne sono individuate in base alle intestazioni, e la corrispondenza proposta può essere
verificata e rettificata prima della conferma. Il formato atteso è illustrato in
[Formato dei file Excel](#formato-dei-file-excel); le colonne non riconosciute, quali note o
ruoli, sono visualizzate come informazioni accessorie a ogni lettura.

All'evento viene attribuita una denominazione, proposta sulla base del titolo del foglio.
Qualora il file indichi dei turni, ne sono richiesti gli orari di inizio e di fine,
precompilati quando ricavabili dall'etichetta (ad esempio `08-12`). Gli eventuali codici fiscali
duplicati sono segnalati in fase di anteprima, senza esclusione di alcun volontario dall'elenco.

Il file di origine non viene in alcun caso modificato: l'applicativo ne conserva una copia, dalla
quale viene generato il registro compilato.

### Registrazione dei passaggi

Nella sezione **Scansione**, a ogni lettura viene visualizzata la scheda del volontario, con
nominativo, ente di appartenenza, stato, turno e squadra. Sono previsti i seguenti accorgimenti,
volti a prevenire gli errori più frequenti:

- due letture della medesima tessera entro tre secondi sono considerate un'unica lettura;
- l'ultima registrazione può essere annullata direttamente dalla scheda del volontario;
- ciascuna giornata è gestita in modo indipendente: un volontario privo di registrazione
  dell'uscita nella giornata precedente risulta regolarmente in ingresso alla prima lettura
  della giornata successiva;
- un arrivo anticipato di almeno un'ora rispetto all'inizio del turno assegnato viene segnalato,
  senza che ciò impedisca la registrazione;
- l'uscita di un volontario cui risulta ancora assegnato del materiale viene segnalata.

### Volontari sprovvisti di tessera o non presenti in elenco

Il campo di scansione consente anche la ricerca per cognome o nome: i risultati sono aggiornati
durante la digitazione, e il volontario viene selezionato con un clic. La pressione del tasto
Invio su un nominativo non determina alcuna registrazione, poiché un medesimo nominativo può
corrispondere a più persone.

Qualora una tessera non corrisponda ad alcun volontario, l'applicativo propone due alternative:

- **l'attribuzione del codice letto a un volontario già presente in elenco**, il cui codice
  fiscale risulti mancante o errato nel file; da quel momento la tessera del volontario viene
  riconosciuta;
- **l'inserimento di un nuovo volontario**, con indicazione di cognome, nome, ente di
  appartenenza e, ove previsti, turno e squadra. Il volontario così inserito compare nel registro
  compilato al pari degli altri.

Un volontario non presente in elenco e sprovvisto di tessera può essere inserito senza codice
fiscale; il codice può essergli attribuito successivamente, alla prima lettura della tessera.

### Situazione in tempo reale

Al di sotto del campo di scansione è riportata la situazione della giornata: una riga per
ciascun volontario atteso, con ente, cognome, nome, turno e orari di ingresso e di uscita,
aggiornata a ogni lettura. La tabella consente di:

- visualizzare separatamente i volontari **presenti**, **usciti** e **assenti**, intendendosi
  per assenti i volontari attesi e non ancora registrati;
- filtrare per ente, cognome o nome durante la digitazione;
- ordinare i dati in base a qualsiasi colonna.

Nella parte superiore sono riportati i totali della giornata e i conteggi per ente. I volontari
registrati in una giornata nella quale non erano attesi sono comunque riportati, con
l'indicazione **non previsto**.

### Eventi su più giornate e turni

Un unico registro può riferirsi a un evento articolato su più giornate. La colonna `DATA` accetta
i formati di uso più comune: una singola data, un elenco di date, un intervallo (ad esempio
`12/08 - 14/08`) o una data con il mese in lettere. Una cella vuota indica un volontario atteso
in tutte le giornate dell'evento. La colonna `TURNO` attribuisce un turno a ciascuna giornata,
ovvero un turno unico valido per tutte.

Nel corso dell'evento:

- il **selettore delle giornate** si apre sulla giornata corrente e consente la consultazione
  delle altre; le letture sono in ogni caso registrate sulla data corrente;
- il **selettore dei turni** si apre sul turno in corso e lo aggiorna in base all'orario, fino
  alla selezione manuale da parte dell'operatore; la situazione e i conteggi sono limitati al
  turno selezionato;
- il turno e la squadra di un volontario possono essere modificati dalla relativa scheda, con
  effetto limitato alla giornata corrente.

### Registro compilato

Il registro compilato è un file Excel generato a partire dalla copia del file importato, del
quale conserva stili, celle unite e impostazioni di stampa. Per ciascun volontario riporta numero
progressivo, ente, cognome, nome e codice fiscale, seguiti dagli orari:

- negli eventi articolati su più giornate, a ciascuna giornata corrispondono specifiche colonne
  di ingresso e di uscita, sotto un'intestazione recante la data;
- i rientri successivi al primo sono riportati in colonne aggiuntive (`ORA INGRESSO 2`,
  `ORA USCITA 2` e seguenti), create solo ove necessario.

Le colonne di carattere organizzativo del file di origine, quali giornate, turni e squadre, non
sono riportate. Il registro può essere generato in qualsiasi momento ed è prodotto
automaticamente alla chiusura dell'evento. Ciascuna esportazione genera un nuovo file, senza
sovrascrivere le precedenti.

### Consegna del materiale

La sezione **Materiale** consente di registrare la consegna ai volontari di apparati radio e di
altre attrezzature. Il materiale non richiede codici a barre: è sufficiente la lettura del
tesserino del volontario, a seguito della quale si apre la relativa scheda con il materiale già
assegnato. L'operatore seleziona gli oggetti da consegnare e indica il recapito telefonico e la
postazione del volontario per la durata dell'evento.

- L'inventario si costituisce alla prima consegna, ovvero può essere predisposto in anticipo,
  anche mediante importazione da file Excel ([formato](#inventario-del-materiale)).
- Consegne e rientri possono essere annullati.
- Il materiale non restituito viene segnalato all'uscita del volontario e alla chiusura
  dell'evento.

Il **riepilogo Excel** riporta, per ciascun volontario cui è stato consegnato del materiale, gli
orari di ritiro e di restituzione di ogni oggetto, ed è generato automaticamente alla chiusura
dell'evento. Il materiale non compare nel registro delle presenze.

### Storico degli eventi

Ciascun registro caricato rimane disponibile nella sezione **Eventi**, unitamente ai relativi
volontari e passaggi. Il caricamento di un nuovo file determina la chiusura del registro
precedente, senza cancellarlo. Per ciascun evento concluso è possibile:

- esportare il registro compilato in qualsiasi momento;
- modificarne la denominazione;
- riaprirlo per la registrazione di ulteriori passaggi, che riporteranno data e ora correnti;
- eliminarlo definitivamente, unitamente a volontari, passaggi e materiale.

Gli eventi conclusi sono consultabili in sola lettura fino all'eventuale riapertura.

### Protezione mediante password

Le operazioni di sostituzione, riapertura, chiusura ed eliminazione di un registro sono protette
da password: l'accesso alla sezione **Eventi**, l'accesso alla sezione **Registro** in presenza
di un evento in corso e la chiusura dell'evento. La password è definita al primo accesso, è
conservata esclusivamente in forma di impronta crittografica e deve essere inserita una sola
volta per sessione. La reimpostazione richiede l'eliminazione del file `passcode.json` dalla
cartella `%LOCALAPPDATA%\RegistraPresenze` del computer della postazione.

Le funzioni di scansione, ricerca, consultazione della situazione ed esportazione non richiedono
la password, al fine di non ostacolare l'operatività della postazione. La protezione è
finalizzata a prevenire operazioni involontarie e non sostituisce il controllo degli accessi al
computer.

## Riservatezza dei dati

I dati trattati, ivi compresi i codici fiscali, risiedono esclusivamente sul computer della
postazione. L'interfaccia è accessibile tramite browser, ma non è raggiungibile da altri computer
della rete. Non sono previsti account né servizi cloud: l'unica connessione effettuata è quella
destinata allo scaricamento degli aggiornamenti.

L'applicativo e i dati sono conservati nella cartella `%LOCALAPPDATA%\RegistraPresenze` dell'utente
di Windows, che contiene il database `presenze.db`, i registri compilati (`export\`), le copie dei
file caricati (`source\`), le copie di sicurezza del database (`backup\`) e il file di
diagnostica.

Ai fini della copia di sicurezza si raccomanda l'esportazione del registro. Il database opera in
modalità WAL, per cui le registrazioni più recenti possono risiedere nel file `presenze.db-wal`:
un'eventuale copia del database deve pertanto comprendere i file `presenze.db`, `presenze.db-wal`
e `presenze.db-shm`, ed essere effettuata ad applicativo chiuso.

## Requisiti

- Computer con sistema operativo Windows.
- Lettore di codici a barre USB.
- Connessione a internet, facoltativa e necessaria esclusivamente per gli aggiornamenti.

## Configurazione del lettore

Il lettore deve essere configurato in modalità **emulazione tastiera**, con **suffisso Invio** e
**senza prefisso**.

- Qualora venga letto il codice a barre del numero di tessera in luogo di quello del codice
  fiscale, l'applicativo lo segnala esplicitamente. In caso di qualsiasi altra lettura non valida
  vengono visualizzati i caratteri ricevuti, utili alla verifica della configurazione del
  lettore.
- Poiché il lettore immette i caratteri nel campo attivo, la perdita del fuoco da parte del campo
  di scansione è segnalata da un indicatore rosso.
- Le finestre di conferma si aprono con il fuoco sul pulsante di annullamento, affinché una
  lettura accidentale non possa confermare una chiusura o un'eliminazione.

## Installazione

1. Scaricare il file `RegistraPresenzeInstaller.exe` dall'[ultima versione](../../releases/latest).
2. Avviarlo con un doppio clic. L'applicativo viene installato nella cartella
   `%LOCALAPPDATA%\RegistraPresenze` dell'utente, senza necessità di privilegi di amministratore;
   sul desktop viene creato il collegamento **Apri Registra Presenze**, da utilizzare per gli
   avvii successivi, e l'applicativo viene aperto.
3. Il file scaricato può quindi essere eliminato.

Qualora sul computer sia presente una versione precedente alla 0.12.0, i dati contenuti nella
cartella `Dati` sono trasferiti automaticamente nella nuova posizione, e la vecchia cartella viene
rimossa. Un'installazione esistente non viene in alcun caso sostituita con una versione meno
recente.

Al primo avvio Windows potrebbe segnalare un'applicazione non riconosciuta; in tal caso è
sufficiente selezionare *Ulteriori informazioni* e successivamente *Esegui comunque*. La
segnalazione è dovuta all'assenza di una firma digitale Windows sull'eseguibile; gli
aggiornamenti automatici sono in ogni caso verificati mediante una firma propria, descritta di
seguito.

## Aggiornamenti

Gli aggiornamenti avvengono in modo automatico e non sono in alcun caso installati durante un
evento. Le nuove versioni vengono scaricate in background e installate esclusivamente in assenza
di un evento in corso: all'avvio dell'applicativo, ovvero immediatamente dopo la chiusura
dell'evento. La disponibilità di una nuova versione è indicata accanto al numero di versione,
nella parte superiore sinistra dell'interfaccia. I dati non sono interessati dall'aggiornamento
e, in assenza di connessione, l'applicativo continua a funzionare regolarmente.

## Versioni firmate

Ciascuna versione pubblicata comprende, oltre a `RegistraPresenzeInstaller.exe`, l'eseguibile
`RegistraPresenze.exe`, destinato all'aggiornamento automatico, e i file `manifest.json` e
`manifest.sig`. Il primo riporta versione, impronta e dimensione dell'eseguibile; il secondo ne
costituisce la firma digitale. Un aggiornamento è installato soltanto se la firma risulta valida
e l'eseguibile corrisponde all'impronta dichiarata. I due file non sono necessari ai fini
dell'installazione manuale.

## Avvertenze e limitazioni

- Gli orari registrati corrispondono a quelli dell'orologio di sistema, che deve essere
  verificato prima dell'inizio dell'evento.
- L'applicativo è destinato a una singola postazione e non è accessibile da altri computer della
  rete.
- Non è consentita la registrazione di passaggi relativi a giornate già trascorse.
- I dati anagrafici non sono sottoposti a validazione: il file Excel si presume corretto, e sono
  segnalati unicamente i codici fiscali duplicati.
- Le rettifiche del codice fiscale effettuate durante l'evento sono conservate nel database; il
  registro compilato riporta il codice presente nel file di origine.
- Il registro compilato non deve essere reimportato: ogni nuovo caricamento deve avvenire a
  partire dal file di origine.
- Per registri estesi su più pagine o relativi a numerose giornate si raccomanda la verifica
  dell'anteprima di stampa. L'intestazione è ripetuta su ciascuna pagina solo se così impostato
  nel file di origine, e la stampante selezionata non viene conservata.
