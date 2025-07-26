# Tesi triennale - Sicurezza dei Sistemi e delle Reti Informatiche

**Integrazione di Large Language Models per il supporto decisionale nella Security Assurance** - Università degli Studi di Milano


Il documento riassume problemi, obiettivi, soluzioni, valutazioni e conclusioni del tirocinio svolto presso il SEcure Service-oriented Architecture Research Lab (SESARlab). 

## SESARlab

Il laboratorio svolge attività di ricerca in ambito *Cloud Computing* e architetture orientate ai servizi. Di particolare interesse è l'implementazione della *Security Assurance*, ovvero la garanzia giustificabile che un sistema sia adeguatamente protetto e funzionante attraverso controlli implementati e verificati in modo continuo. Il tirocinio è stato svolto in collaborazione con il gruppo di sviluppo della piattaforma Moon Cloud, finalizzata alla realizzazione della Security Assurance per sistemi distribuiti. 

## Contesto iniziale

Moon Cloud è una piattaforma *Platform as a Service* in cui i controlli sono implementati attraverso script (sonde) che ricevono in input un elenco di dati necessari per la loro esecuzione (configurazione). Obiettivo della piattaforma è la capacità di fornire *compliance* a standard e normative (ad esempio GDPR o HIPAA). La selezione e configurazione delle sonde è ad oggi manuale, ripetitiva e soggetta a errori, soprattutto nei casi di compliance normativa. Gli operatori sono tenuti a conoscere la totalità delle sonde disponibili e le relative caratteristiche, dovendo selezionare quelle adeguate per specifici controlli previsti dalle normative tecniche. 

## Obiettivi del lavoro

L'obiettivo principale è valutare la fattibilità dell'uso di modelli linguistici generativi (LLM) per automatizzare la selezione e configurazione delle sonde, sviluppando un sistema di supporto decisionale (DSS) che riduca il carico sull'operatore. La ricerca si articola in tre fasi: (i) progettazione del DSS; (ii) realizzazione di una metodologia a supporto delle analisi e (iii) valutazione delle prestazioni attraverso *Proof-of-Concept* (PoC) sviluppato. 

Un elemento centrale dello studio è l'uso di modelli compatti open-source, in alternativa ai grandi modelli commerciali, perseguendo obiettivi di sostenibilità economica e maggiore controllo sulla riservatezza dei dati.

Lo studio si inserisce nel contesto delle applicazioni dei LLM in sistemi di supporto alle decisioni, già analizzate in ambiti come medicina, economia, sicurezza informatica e conformità normativa. A differenza degli studi precedenti, si propone un approccio sistematico alla selezione automatizzata di controlli per la Security Assurance, offrendo soluzioni alternative rispetto ai limiti riscontrati in parte della letteratura.

## Lavoro svolto

Una fase preliminare ha riguardato lo studio dell'anatomia delle sonde  e lo sviluppo di una suite di controlli per verifiche sul broker MQTT VerneMQ, arricchendo il catalogo utilizzato nelle fasi successive.

È stata quindi delineata un'architettura in cui l'utente inserisce le richieste tramite dashboard, il sistema compone un *prompt* a partire da un template e da un catalogo sonde, applicando tecniche di In-Context *Retrieval Augmented Generation* (In-Context RAG). Per ciascun controllo selezionato il processo si ripete per la fase di configurazione della sonda. L'operatore ottiene in tal modo una suite di controlli proposti e pre-configurati. 

Successivamente si è definita una metodologia contenente:  
(i) classificazione delle richieste che l'operatore può effettuare;  
(ii) gestione delle informazioni necessarie alla generazione;  
(iii) tipologie e progettazione di prompt;  
(iv) prompt specifici per i diversi task di selezione e configurazione;  
(v) supporto ai framework di sicurezza, inclusa l'estensione dello standard per la documentazione di sonde;  
(vi) strumenti per la valutazione delle performance, tra cui un sistema di classificazione dei dataset e di metriche per la valutazione.

Sono state analizzate strategie di miglioramento, soffermandosi sul *prompt engineering* piuttosto che sulla modifica dei parametri del modello. Il secondo approccio ha infatti dimostrato limitazioni rispetto al fenomeno di aggiornamento continuo della conoscenza.

Sono state analizzate le problematiche dettate dalla generazione dei dataset e dalla necessità di un approccio *human-in-the-loop* nel processo di valutazione dei risultati. La valutazione proposta si è basata dunque su un *walkthrough* rappresentativo della variabilità delle performance a fronte di tecniche di prompt engineering, mostrando la possibilità di ottenere un output gradualmente più simile all'output ideale attraverso la sola manipolazione dell'input.  

Una seconda valutazione qualitativa si è basata su un approccio *LLM-as-a-judge*: a partire da un dataset generato seguendo le regole definite, è stato utilizzato un modello più performante per valutare i risultati ottenuti mediante prompt con diversi livelli di informazione, dimostrando come sia effettivamente possibile migliorare le risposte per un compito specifico, usando un modello di dimensioni limitate e soprattutto senza necessità di modificare i parametri del modello. Per le misurazioni è stato realizzato un PoC in Python, accessibile via API e interfaccia web ed ospitato su VM GPU del laboratorio.

In maniera marginale, sono stati infine affrontati scenari di integrazione completa con Moon Cloud per offrire automatizzazione nel deployment dei controlli selezionati. Sono state analizzate le possibili vulnerabilità (es. *prompt hacking*), evidenziando alcune potenziali problematiche e suggerendo l'aggiornamento del threat model della piattaforma.

## Sviluppi futuri e conclusioni

Futuri sviluppi riguarderanno la generazione dei dataset e l'esecuzione di benchmark ufficiali, la ricerca di modelli open-source più prestanti, la sperimentazione con prompt differenti e il miglioramento del supporto agli standard. Ulteriore direzione è quella del fine-tuning dei modelli per l'integrazione di conoscenza del settore Cybersecurity e successiva analisi delle prestazioni. Di interesse anche la completa integrazione con Moon Cloud per realizzare il deployment automatico delle sonde selezionate. 

Il tirocinio ha costituito un'importante opportunità per approfondire il funzionamento e l'applicazione di una tecnologia emergente, attraverso un approccio rigoroso e scientifico. Sono state gettate le basi per sviluppi applicativi futuri e si conferma la validità della soluzione proposta, pur riconoscendo l'importanza di un esperto nel valutare i risultati generati.
