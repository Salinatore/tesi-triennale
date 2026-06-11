Constesto generale:
Scrittura di documento di tesi triennale. Prima della tesi ho svolto un tirocinio in cui ho preso un progetto preesistente e ho creato un modulo aggiuntivo aumentarne le capacità. Nella mia tesi devo descrivere tutto il lavoro svolto durante il tirocinio. Il progetto preesistente di cui parlo riguarda la demo, per l'argomento di aggregate computing, mostrato dal gruppo di ricerca dove ho fatto tirocinio durante la notte europea dei ricercatori.

## Indice

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
  - **Modellazione delle Entità**  
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

## Preferenze di scrittura
- Lingua: italiano
- Formato output: LaTeX (solo il corpo della sezione, senza preambolo)
- Livello: tesi triennale, tono formale ma non eccessivamente accademico
- Stile: fluido e narrativo, non elenchi puntati nel corpo del testo
- Figure: incluse inline dove architetturalmente rilevanti
- Citazioni: usare chiavi coerenti con quelle già usate nelle sezioni
  precedenti; non citare lo stesso paper più volte per ogni singolo concetto,
  ma una volta sola nel punto più naturale
- Testo: senza line break manuali nel sorgente
