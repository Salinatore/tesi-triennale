## Slide 1 — Titolo 

Buongiorno. Il titolo della mia tesi è "Progettazione di un framework protocol-agnostic per il coordinamento di sciami nel contesto di Project Emerge".

---

## Slide 2 — Background: Project Emerge 

Partendo dal contesto, Project Emerge è un dimostratore open-source che porta l'Aggregate Computing dall'ambito puramente teorico a un'implementazione reale, applicata al coordinamento di sciami robotici.

L'Aggregate Computing è un paradigma che permette di programmare uno sciame di dispositivi eterogenei come se fosse un'unica entità collettiva, senza bisogno di un controllo centralizzato: ogni dispositivo esegue localmente lo stesso comportamento, e dal loro insieme emerge il comportamento globale dello sciame.

Dal punto di vista architetturale e implmentativo, il sistema è organizzato in quattro moduli centralizzati, ciascuno responsabile di una mansione specifica, e robot.  

---

## Slide 3 — Connessioni tra i moduli 

Come è possibile vedere in questo schema tutte queste entità parlano tra loro tramite MQTT. È importante notare questa scelta archietturale perché è su questa che si base il mio lavoro.

---

## Slide 4 — Analisi: obiettivi, vincoli e requisiti 

L'obiettivo del mio lavoro è stato rendere il sistema protocol-agnostic, cioè permettere a client eterogenei — con esigenze e tecnologie diverse — di interagire con il sistema, indipendentemente dal protocollo che utilizzano.

Questo obiettivo doveva però rispettare due vincoli fondamentali: non potevo modificare i moduli esistenti di Emerge, e per questo MQTT doveva rimanere il protocollo di comunicazione interno tra i moduli.

A partire da questi vincoli ho definito i requisiti. Dal punto di vista funzionale, il sistema doveva esporre più protocolli eterogenei, supportando sia lo stile event-driven, come MQTT, sia per request/response e doveva essere pensato per un'estendibilità futura. Dal punto di vista non funzionale, data la natura IoT del sistema, doveva essere capace gestire molte connessioni simultanee, garantire basse latenze, essere estendibile con altri protocolli senza riscrivere il nucleo del sistema, ed essere facilmente testabile.

---

## Slide 5 — Modello di dominio

Prima di progettare la soluzione, ho definito un modello di dominio che identifica le entità principali coinvolte e le loro relazioni. Questo schema è stato la base concettuale su cui sono state poi costruite le risorse esposte dai pari protocolli implementati.

---

## Slide 6 — Il domain gateway 

La soluzione che ho progettato si basa sull'introduzione di un unico modulo aggiuntivo, il domain gateway, che si frappone tra il broker MQTT e i client eterogenei, mediando, tra loro, la comunicazione.

Questa scelta porta con sé diversi vantaggi. Prima di tutto, i moduli esistenti restano completamente invariati. In secondo luogo, se in futuro servisse supportare un nuovo protocollo, sarebbe sufficiente intervenire solamente sul gateway, senza toccare il resto del sistema. Infine, grazie a una cache interna, il gateway riesce a supportare sia la notifica continua sia lo stile request/response, anche se il broker MQTT di per sé lavora solo per notifica.

Nella figura, in rosso, sono evidenziate proprio le componenti aggiunte rispetto all'architettura originale di Emerge.

---

## Slide 7 — Struttura interna del gateway

Entrando nel dettaglio, il gateway è organizzato internamente attorno a tre elementi chiave: le connessioni, che rappresentano tutti i protocolli. Due bus — uno inbound e uno outbound — che gestiscono il flusso dei messaggi dall'interno verso l'esterno e viceversa. E infine la cache che, come ho citato prima, mantiene lo stato più recente del sistema per permettere di rispondere anche alle richieste di tipo request/response.

---

## Slide 8 — Implementazione 

Per l'implementazione ho scelto Python 3.13 con asyncio, per gestire in modo efficiente le connessioni concorrenti, insieme a varie librerie che supportano questa modalità.

Le interfacce e classi principali del sistema sono Connection, Bus, Cache e Container: quest'ultimo è il componente che orchestra tutti gli altri, come mostrato nella figura a destra. Il Container, dopo aver istanziato Bus e Cache, li inietta nelle connessioni tramite Dipendency Injection nel costruttore, questo sarà utile in fase di testing.

Attualmente il gateway espone protocolli basati sia su TCP che UDP, ciascuno dei quali supporta sia la modalità a notifica che request/response: HTTP e WebSocket per TCP, CoAP per UDP (attraverso la modalità Observe). Questo dimostra la capacità del sistema di gestire un’ampia eterogeneità di protocolli.

---

## Slide 9 — Valutazione: testing automatico

Per la validazione del sistema, coma anticipato, un aspetto chiave è stata la Dependency Injection, che mi ha permesso di iniettare connessioni mock e isolare facilmente ogni singolo componente, senza dover modificare il codice applicativo.

I test automatici sono organizzati per protocollo, e per isolare completamente la logica dal broker reale ho utilizzato una MockMQTTConnection, iniettata al posto della connessione MQTT reale.

Sono stati realizzati 80 test, che hanno permesso una copertura complessiva dell'88% del codice.

---

## Slide 10 — Conclusione 

In conclusione, il lavoro svolto ha raggiunto gli obbiettivi, rispettando i vincoli e soddisfatto sia i requisiti funzionali che quelli non funzionali definiti in fase di analisi.

Come sviluppi futuri, vedo diverse direzioni: testare il sistema con una prova reale, valutare una sostituzione graduale di MQTT come protocollo interno, aggiungere supporto a nuovi protocolli, e infine esplorare soluzioni di replicazione del modulo attraverso, load balancing e cache distribuita.

---

## Slide 11 — Chiusura

Grazie per l'attenzione. 