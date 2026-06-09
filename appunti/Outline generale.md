Ho pensato di seguire l'indice che propone il Prof. Pianini dentro al template.

- **Introduzione**  
  Presentazione sintetica del lavoro: obiettivo della tesi, contributo principale (gateway IoT estendibile) e struttura del documento.

- **Background**
   - **Studio dell’Aggregate Computing**  
    Sintesi dei concetti appresi (programmazione aggregata, riferimento a letteratura scientifica) e loro relazione con il contesto di partenza.
   - **Progetto allo stato attuale** 
	Descrizione del progetto alla stato iniziale, i suoi moduli, le tecnologie usate e soprattutto dei suoi limiti.

- **Analisi**
  - **Obbiettivi**  
    Elenco puntato degli obiettivi, come:  
    – Realizzare un gateway che unifichi l’accesso a robot eterogenei.  
    – Consentire l’aggiunta di nuovi protocolli senza modificare il nucleo.  
    – Garantire responsività anche con molti client connessi.
  - **Vincoli**  
    Elenco delle restrizioni imposte: linguaggi/parti del sistema non modificabili, viscosità legata a MQTT come broker centrale.
  - **Requisiti funzionali e non funzionali**  
    - *Funzionali*: server HTTP REST, endpoint WebSocket, CoAP, comunicazione con il server interno.  
    - *Non funzionali*: estendibilità dei protocolli senza riscrivere il nucleo (es. nuovo protocollo integrabile senza riscrivere interamente il modulo), responsività sotto carico, manutenibilità generale.
  - **Modello del Dominio**  
    Individuazione delle entità chiave, le relazioni e diagramma UML riassuntivo.

- **Progettazione**
  - **Architetturale rispetto al sistema**  
    Alternative esaminate, alternativa scelta e motivazione.
  - **Architetturale di dettaglio dell’applicativo**  
    Definizione delle interfacce, nucleo riutilizzabile, astrazione della connessione, bus interni per lo scambio messaggi, definizione api per ogni protocollo da implementare. 

- **Implementazione**
  - **Organizzazione del codice e stack tecnologico**  
    Struttura dei moduli, linguaggio adottati, librerie principali e loro ruolo.
  - **Server di protocollo realizzati**  
    Dettagli su HTTP REST, WebSocket, CoAP e MQTT.

- **Valutazione**
  - **Testing automatico**  
    Strategia di test (api), framework impiegati, copertura, uso di mock.
  - **Dimostrazione sperimentale**  
    Da definire.

- **Conclusione e Sviluppi Futuri**  
  Riepilogo dei risultati raggiunti, limiti attuali, possibili evoluzioni.

- **Bibliografia**  
  Riferimenti organizzati per tipologia:  
  - Letteratura scientifica su aggregate computing.  
  - Standard e RFC (MQTT, CoAP RFC 7252, WebSocket RFC 6455).  
  - Documentazione delle librerie e tecnologie usate.  