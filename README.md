# BALTUR
WEB Order Entry (di seguito portale OE
LOGIN UTENTE

Ogni utente sarà dotato di Username e Password per effettuare l'accesso al portale.

Potrà resettare autonomamente la sua password tramite apposita procedura (vedi esempio Fig.1)

Fig.1

In caso l'utente abbia necessità di resettare la password dovrà cliccare sul link Password Reset si aprirà una box dove verrà richiesto di inserire il proprio Username. Cliccando Password Reset

il sistema esegue gli step seguenti:

- recupero indirizzo mail utente utilizzando lo username in chiave (query su tabella OE_UTENTI nel database del portale OE) - invio mail con link di password reset nella forma: http://nomesito/passwordreset?token

- cliccando sul link, l'utente viene redirezionato sulla pagina di inserimento nuova

password. (Fig.2)

Fig.2

Qualora le due password inserite siano coincidenti, il sistema eseguirà il login utente persentando la pagina di home, in caso contrario verrà mostrato, all'utente, un messaggio di errore.

3 HOME PAGE UTENTE

Gli utenti del sistema possono essere di due tipologie:

- Cliente

- Agente di vendita (gestisce n-clienti)

Dopo aver effettuato il login l'utente visualizza la propria home page, Fig.3

Fig.3

Nell'esempio di Fig.3 è mostrata la home di un Agente di vendita con l'elenco dei clienti per i quali può effettuare ordini nel portale OE.

Nel caso l'utente sia un cliente, la home mostrerà una sola riga contentente i dati dell'utente che ha fatto il login con la possibilità di creare nuovi ordini e gestire gli ordini pregressi.

Sulla home sono presenti i link per:

- accedere alla scheda anagrafica del cliente;

- accedere allo storico ordini e storico spedizioni

- accedere direttamente agli ordini in stato: Aperto, In attesa, Da ricevere

- effettuare un nuovo ordine di tipo: Manualistica, Gadgets, Ricambi, Ventola

4 ANAGRAFICA CLIENTE

Dalla pagina di home, cliccando sul link del codice cliente (colonna Anagrafica) ad esempio C00015756 si accede ai dati anagrafici del cliente, Fig.4.

Tutte le informazioni anagrafiche del cliente sono in sola lettura, quindi non sono modificabili.

Fig.4

5 STORICO ORDINI

Dalla home, cliccando il bottone è possibile accedere alla pagina dello Storico ordini. Fig.5

Fig.5

Nella pagina di Storico ordini è possibile:

- accedere alla lista degli ordini con possibilità di visionarli e modificarli se lo stato lo permette (Aperto).

- Visualizzare il pdf della conferma d’ordine se l’ordine è confermato (definire con KnowHow il web service da chiamare per visualizzare il pdf)

- Possibilità di filtrare gli ordini per tipo, stato e numero. Dopo aver applicato il filtro viene mostrato l'elenco degli ordini in tale stato e il numero degli ordini presenti in tale stato.

6 STORICO SPEDIZIONI

Dalla home, cliccando sul bottone è possibile accedere alla pagina dello Storico spedizioni. Fig.6

Fig.6

Nella pagina dello Storico spedizioni è possibile:

- visualizzare il pdf della bolla (DDT) se la spedizione è confermata (definire con KnowHow il web service da chiamare per visualizzare il pdf)

- visualizzare il tracking number se presente

INSERIMENTO NUOVO ORDINE

Per poter inserire un nuovo ordine bisogna selezionare una delle quattro icone che rappresenta il tipo di ordine da eseguire:

- Manualistica

- Gadgets

- Ricambi

- Ventola

Fig.7

Nella pagina di Nuovo ordine è possibile:

- visualizzare le informazioni anagrafiche del cliente (le informazioni non sono modificabili)

- modificare delle informazioni legate all’ordine (vedi informazioni con combobox, in rosso, o con campi di testo). I dati necessari al popolamento delle combobox verranno caricati da opportune tabelle rese disponibili in INFOR LN

- visualizzare e modificare il codice articolo, la quantità e la data di spedizione del materiale da Baltur; il resto delle informazioni non è modificabile e deriva dall’anagrafica articolo o da contratto

- visualizzare un’indicazione visiva verde in funzione della formula: data inserita nel campo - data in cui l’utente manutenziona l’ordine > tempo che Baltur impiega per rendere disponibile l’articolo. Nel caso contrario l'indicazione visiva sarà di colore rosso. Qualsiasi altra informazione che l'utente voglia inserire a corredo dell'ordine dovrà essere scritta nel campo note. Sarà consentito l'invio dell'ordine a Baltur anche in presenza di articoli con indicazione visiva rossa

- visualizzare il totale dell’ordine aggiornato ad ogni inserimento riga

- inserire nuove righe conoscendo il codice articolo o ricercando l'articolo per descrizione; in caso di articoli sostituiti mostrare un messaggio all’utente e inserire il nuovo codice/i. Come deve essere effettuata la ricerca dell'articolo mediante codice / descrizione? Tramite invocazione di un webservice? Tramite query su vista? Tramite query su tabella? Come devono essere gestiti gli articoli sostituiti?

- eliminare le righe ordine

- salvare l'ordine in stato aperto per una successiva modifica (salvataggio su db del portale OE)

- stampare l'ordine

- inoltrare l’ordine a Baltur congelando tutti i dati (salvataggio su db del portale OE + invio a INFOR LN via webservice)

- chiudere la pagina di inserimento nuovo ordine senza salvare i dati (Esci senza salvare)

8 RICERCA DEGLI ARTICOLI

La ricerca dell'articolo da inserire nell'ordine può essere eseguita per codice articolo, qualora lo si conosca, oppure cliccando sull'icona della lente presente nella riga di inserimento articolo in ordine.

Fig.8

Dopo aver selezionato la lente si apre un form di ricerca articolo utilizzando come campi chiave il codice articolo oppure la descrizione articolo, in ogni caso le query di ricerca verranno fatte utilizzando l'operatore LIKE '%testodiricerca%'. Fig.8

9 VISUALIZZAZIONE DELLA SCHEDA ANAGRAFICA DEL PRODOTTO

Qualora la ricerca dell'articolo mostri dei risultati, è possibile visualizzare la scheda anagrafica del singolo articolo cliccando sul codice relativo. Fig.9

Fig.9

La scheda di visualizzazione dell’anagrafica del prodotto contiene: nome prodotto, descrizione, eventuale descrizione estesa, eventuale immagine, eventuale pdf scaricabile, numero di giorni in cui Baltur garantisce disponibilità del prodotto.

I prezzi, gli sconti e i prodotti vanno filtrati e gestiti secondo i listini o le eventuali promozioni a cui il cliente, inserito nella testata dell'ordine, ha diritto.

10 TABELLA OE_UTENTI – TRACCIATO RECORD

idutente username password (MD5) data inizio validita data fine validita stato ruolo email token reset pwd

A fronte della tabella OE_UTENTI, è necessario avere una vista nel database di INFOR LN tale che per ciascun utente in OE_UTENTI si possa recuperare l'anagrafica, qualora si tratti di utente con ruolo 'Cliente'.

Nel contempo, qualora l'utente in OE_UTENTI abbia ruolo 'Agente di vendita', è fondamentale recuperare da INFOR LN la struttura di tipo master-detail rappresentante i clienti associati all'Agente di vendita, in modo da popolare la home page dell'utente. Fig.3

Sul db di LN deve essere creata una tabella (in carico a Baltur) tale che, per ciascun cliente richiamabile in un ordine, ci sia evidenza di quale tipologia di ordini, il cliente è abilitato a compiere. Si tratta, fondamentalmente, di una tabella di assegnazione permessi nella forma:

idutente manualistica gadgets ricambi ventola

SI / NO SI / NO SI / NO SI / NO

11 ASPETTI TECNICI DA DISCUTERE CON KNOWHOW

I seguenti aspetti tecnici devono essere chiariti con un referente lato KnowHow:

- definizione del webservice e modalità di invocazione, per richiamare eventuali pdf (ordini, ddt, …)

- inserimento nuovo ordine Fig.7 bottone Invia a Baltur. L'utente ha completato la definizione del proprio ordine, attiva la call to action 'Invia a Baltur', a valle deve essere invocato un webservice di INFOR LN affinche l'ordine sia sottomesso a LN. Si richiede la definizione del webservice e modalità di invocazione.

- in Fig.5 si visualizza lo stato degli ordini del cliente, tralasciando lo stato 'Aperto' gestibile direttamente dal portale OE, si richiede che INFOR LN 'informi' il portale OE circa lo stato attuale di lavorazione di ciascun ordine, appena l'ordine stesso, in carico a INFOR LN, subisce una nuova fase di lavorazione. Come gestire quindi tutti i flussi di ritorno di INFOR LN verso il portale OE? Una ipotesi è quella di definire delle tabelle di frontiera gestite da LN dove, in modalità schedulata, il portale OE andrà a leggere l'aggiornamento di stato per ciascun ordine.

- un ordine creato dal portale OE e inviato a Baltur potrebbe svilupparsi in INFOR LN in un numero n di ordini, anche in questo caso è fondamentale definire:

- la modalità con cui INFOR LN 'informerà' il portale OE dell'avvenuto split dell'ordine

- la modalità di visualizzazione, da parte del portale OE, sia dell'ordine originario inviato a INFOR LN, sia degli n ordini in cui l'ordine originario è stato suddiviso

- in fase di inserimento di un nuovo ordine Fig.7 ci sono alcune informazioni da specificare mediante scelta da lista a discesa (combobox). Tali liste andranno popolate mediante query su tabelle opportunamente create in INFOR LN, le tabelle dovranno essere:

- Termini di consegna

- Spedizione tramite

- Spedizioniere

- Attrezzi a corredo della consegna (Sponda idraulica)

- in fase di ricerca di un articolo Fig.8 è possibile visualizzare gli articoli corrispondenti al criterio di ricerca solo se appartengono al/ai listino/i associato/i al cliente che esegue l'ordine. Come deve avvenire la fase di ricerca degli articoli? Possibili proposte da discutere possono essere:

- mediante invocazione a webservice di INFOR LN

- mediante query su una vista ne db di INFOR LN

- mediante query su tabelle di INFOR LN

- può presentarsi l'eventualità che il cliente richieda, in un ordine, un articolo fuori produzione, a tal proposito bisogna stabilire se informare il cliente che l'articolo richiesto è fuori produzione, sostituire l'articolo richiesto con un articolo equivalente oppure entrambe le cose
