
# Rischi dell'utilizzo di AI senza governance

---
>[!WARNING]
> *"L'adozione dell'AI sta superando di gran lunga la governance dell'AI. Le organizzazioni che sorpassano sicurezza e governance in favore di un'adozione immediata stanno pagando un prezzo molto alto."*
> — [IBM Cost of a Data Breach Report, Luglio 2025](https://newsroom.ibm.com/2025-07-30-ibm-report-13-of-organizations-reported-breaches-of-ai-models-or-applications,-97-of-which-reported-lacking-proper-ai-access-controls)

---

## 1. Shadow AI e governance mancante

Prima ancora di analizzare le vulnerabilità tecniche, esiste un rischio organizzativo che molte aziende ignorano: il team **sta già usando** strumenti AI non approvati.

Una [survey su 2.000 dipendenti in USA e UK condotta da CSO Online (2025)](https://www.csoonline.com/article/4111384/top-5-real-world-ai-security-threats-revealed-in-2025.html) ha rilevato che il **49% usa strumenti AI non approvati dai propri datori di lavoro** e che oltre la metà non capisce come i propri input vengano archiviati e analizzati da questi tool.

Le conseguenze di questa "Shadow AI" sono misurabili in termini economici. Il [Cost of a Data Breach Report 2025 di IBM](https://newsroom.ibm.com/2025-07-30-ibm-report-13-of-organizations-reported-breaches-of-ai-models-or-applications,-97-of-which-reported-lacking-proper-ai-access-controls) — basato su 600 organizzazioni compromesse — ha rilevato che **1 azienda su 5 ha subito una violazione dovuta a Shadow AI**, con un costo medio della violazione di **$670.000 superiore** rispetto alle violazioni standard ($4,63M vs $3,96M). La Shadow AI è ora uno dei tre fattori di costo più elevati nei data breach.

Ma, oltre alle misurazioni di perdite economiche che sono relative e riguardano diversi aspetti aziendali, c'è un dato più preoccupante **"la governance e controllo"**: il **63% delle organizzazioni violate non ha una policy di governance AI o la sta ancora sviluppando**. Di quelle che ce l'hanno, solo il **34% effettua audit regolari per rilevare l'uso di AI non approvata**.

---
> [!WARNING]
> Se la nostra organizzazione non ha ancora una policy formale sull'uso degli AI tools, statisticamente il team sta già usando strumenti non approvati con accesso al codice sorgente aziendale [-](https://www.csoonline.com/article/4111384/top-5-real-world-ai-security-threats-revealed-in-2025.html).

---

## 2. Il Codice AI è Codice Insicuro (per Default)

Il secondo rischio riguarda la qualità intrinseca del codice prodotto da modelli AI senza supervisione adeguata.

Il [Veracode 2025 GenAI Code Security Report](https://blog.barrack.ai/every-ai-app-data-breach-2025-2026/) ha testato 80 task di coding su oltre 100 LLM: **quando i modelli AI avevano a disposizione sia un metodo sicuro che uno insicuro, hanno scelto quello insicuro nel 45% dei casi**. Java è risultato il linguaggio più rischioso con un tasso di fallimento sicurezza del 72%. Il Cross-Site Scripting ha fallito nell'86% dei casi. Il Log Injection nell'88%.

Questi numeri non rappresentano bug occasionali. Rappresentano un **pattern sistemico** che non migliora con modelli più grandi o più recenti — indicando che il problema non è di scala ma di architettura fondamentale dei modelli linguistici, che ottimizzano per la plausibilità sintattica, non per la correttezza di sicurezza.

Sul fronte SQL — particolarmente rilevante per il nostro stack su SQL Server — la situazione è analoga: il 40% delle query SQL generate da AI contiene potenziali vulnerabilità di injection. Un singolo endpoint non revisionato con una query AI-generata non parametrizzata può essere il vettore di un attacco all'intero database aziendale.

> [!IMPORTANT]
> Il codice generato da AI non è "abbastanza sicuro da default". È codice che richiede lo stesso livello di review del codice scritto da un junior developer alle prime esperienze. La differenza è che viene prodotto molto più velocemente — il che può amplificare, non ridurre, il debito di sicurezza se la review non scala di conseguenza.

---

## 3. Impatto Amplificato: La Velocità Come Fattore di Rischio

> [!IMPORTANT]
>C'è un paradosso nel cuore degli AI agent per il coding: la stessa caratteristica che li rende così produttivi — la velocità e l'autonomia nell'esecuzione — è quella che amplifica l'impatto degli errori e delle vulnerabilità.

Un developer umano che commette un errore di sicurezza inserisce una vulnerabilità alla volta, nel tempo di scrittura di una funzione. Un AI agent che opera su istruzioni errate o su prompt iniettati può modificare decine di file, invocare API, commitare codice e triggerare pipeline CI/CD in pochi minuti — tutto con la credibilità di un tool "approvato".

Secondo Randall Degges, Head of Developer and Security Relations di [Snyk](https://fortune.com/2025/12/15/ai-coding-tools-security-exploit-software/): *"La supply chain è sempre stata un punto debole per i developer software in particolare. È sempre stato un problema, ma ora è ancora più prevalente con gli AI tools."* La natura agentic degli strumenti amplifica ogni vulnerabilità preesistente nella supply chain.

Un ulteriore vettore spesso sottovalutato è il **typosquatting** potenziato dall'AI: attori malevoli creano package o estensioni AI con nomi quasi identici a quelli legittimi. In [un caso documentato da Fortune nel 2025](https://fortune.com/2025/12/15/ai-coding-tools-security-exploit-software/), un core developer di Ethereum ha visto il proprio crypto wallet svuotato dopo aver scaricato per errore un'estensione malevola per il popolare AI coding tool Cursor. Gli AI tool amplificano questo rischio perché, sempre più spesso, sono loro stessi a suggerire e installare dipendenze.

---

## 4. Gli AI Agent Come Superficie d'Attacco

Quando uno sviluppatore configura un AI agent con accesso al repository, al filesystem locale e agli strumenti di build — come avviene normalmente con Claude Code o con Copilot Chat nella modalità agent — sta creando un **nuovo vettore di attacco** che i tradizionali strumenti di sicurezza non vedono.

### 4.1 Prompt Injection: il Nuovo SQL Injection

Secondo [OWASP Top 10 per LLM Applications 2025](https://www.obsidiansecurity.com/blog/prompt-injection), la **prompt injection è la vulnerabilità critica #1**, presente nel **73% dei deployment AI in produzione** valutati durante audit di sicurezza.

Il meccanismo è semplice da comprendere ma difficile da difendere: un attaccante inserisce istruzioni malevole in dati che l'agente leggerà nel corso normale del suo lavoro — un issue su GitHub, un file di documentazione, un commento in un ticket. L'agente le interpreta come istruzioni legittime e le esegue.

**Maggio 2025 — GitHub MCP Data Heist:** [Invariant Labs ha dimostrato una vulnerabilità critica nel Model Context Protocol (MCP) di GitHub](https://securityboulevard.com/2026/02/protecting-ai-security-2025-hot-security-incident/). Un attaccante inseriva comandi malevoli all'interno di Issue pubblici di repository GitHub. Quando l'agente AI veniva invocato per leggere e processare l'issue, eseguiva indiscriminatamente i comandi incorporati, estraendo dati sensibili — **codice sorgente di repository privati e chiavi crittografiche** — e trasmettendoli verso destinazioni controllate dall'attaccante. L'attacco ha aggirato completamente il sistema di controllo dei permessi di GitHub.

La causa tecnica è strutturale: quando un agente esegue azioni utilizzando le credenziali GitHub del developer, **non distingue tra "descrizione del task dell'utente" e "comandi iniettati dall'attaccante"** nell'Issue. Poiché i developer concedono ai propri agenti permessi a livello globale su GitHub, senza segmentazione fine-grained per operazioni di lettura/scrittura/esecuzione, questo permette agli attaccanti di dirottare l'agente locale e rubare dati sensibili.

### 4.2 Vulnerabilità nel Protocollo MCP

Il Model Context Protocol — l'infrastruttura su cui si basano le integrazioni degli agenti con tool esterni — ha rivelato nel 2025 una serie di vulnerabilità critiche che hanno impattato direttamente i developer che usavano AI agent in modo non supervisionato.

**[CVE-2025-6514](https://authzed.com/blog/timeline-mcp-breaches) — Remote Code Execution su 437.000+ ambienti:** JFrog ha divulgato un bug critico in `mcp-remote`, il proxy OAuth usato per connettere i client MCP locali a server remoti. Server MCP malevoli potevano inviare un `authorization_endpoint` che `mcp-remote` passava direttamente alla shell di sistema, ottenendo **remote code execution sulla macchina del developer**. Con oltre 437.000 download e adozione in Cloudflare, Hugging Face e Auth0, la vulnerabilità trasformava qualsiasi installazione non aggiornata in un backdoor della supply chain: un attaccante poteva eseguire comandi arbitrari, sottrarre chiavi API, credenziali cloud, file locali, chiavi SSH e contenuti di repository Git — semplicemente puntando il tool AI verso un endpoint MCP malevolo.

In un [caso separato documentato nella stessa timeline](https://authzed.com/blog/timeline-mcp-breaches), un package MCP che si spacciava per un legittimo "Postmark MCP Server" iniettava **copie BCC di tutte le comunicazioni email** — inclusi documenti confidenziali, memo interni e fatture — verso un server controllato dall'attaccante. Il vettore era la supply chain: un package malevolo nel registro MCP, eseguito con i privilegi elevati tipici dei server MCP.

### 4.3 Tool Poisoning e Attacchi alla Supply Chain

[Ricercatori di Palo Alto Networks Unit 42](https://stytch.com/blog/mcp-vulnerabilities/) hanno dimostrato uno scenario in cui la descrizione di un tool malevolo istruiva l'agente AI a **copiare ogni frammento di codice visualizzato e inviarlo a un server remoto**, senza alcun avviso all'utente. In pratica: ogni volta che un developer usava l'agente con un tool di editing del codice, ogni pezzo di codice poteva essere trasmesso all'attaccante. Come ulteriore vettore, un attacco di "retrieval-agent deception" consisteva nel contaminare la documentazione in modo che, quando l'agente la leggeva, eseguisse comandi nascosti per cercare nel sistema le AWS key e pubblicarle online.

> [!CAUTION]
> Gli strumenti AI agent che utilizzano MCP non sono distinguibili dagli strumenti legittimi sul piano dell'interfaccia utente. Un developer che installa un MCP server da una fonte non verificata — es. un repository GitHub qualsiasi — potrebbe star eseguendo codice che ha accesso completo al suo filesystem, alle sue credenziali e al codice sorgente aziendale.

---

## 5. Il Rischio dei Permessi Eccessivi

Un tema trasversale a tutti gli incidenti documentati è quello dei **permessi eccessivi**: gli agenti AI vengono configurati con accesso molto più ampio del necessario, per convenienza o per mancanza di policy.

Il [Cost of a Data Breach Report 2025 di IBM](https://newsroom.ibm.com/2025-07-30-ibm-report-13-of-organizations-reported-breaches-of-ai-models-or-applications,-97-of-which-reported-lacking-proper-ai-access-controls) ha rilevato che il **97% delle organizzazioni che ha subito una violazione AI non aveva controlli di accesso AI in attività**. Il 60% degli incidenti di sicurezza AI ha portato a **compromissione di dati**, il 31% a **interruzione operativa**.

La logica del "privilegio minimo" — dare ad ogni sistema solo i permessi strettamente necessari per il suo scopo — è un principio consolidato nella sicurezza informatica. Gli AI agent la violano strutturalmente quando vengono configurati dai developer in modo informale: è più semplice dare un Personal Access Token con accesso a tutti i repository che configurare permessi granulari, e in assenza di una policy aziendale, quasi tutti i developer scelgono la strada più rapida.

[Ricercatori di Check Point e Lakera, nell'analisi del Q4 2025](https://www.esecurityplanet.com/artificial-intelligence/ai-agent-attacks-in-q4-2025-signal-new-risks-for-2026/), hanno documentato che **gli attacchi indiretti che sfruttano le capacità degli agenti** — navigazione web, accesso a documenti, chiamate a tool — **hanno successo con meno tentativi e impatto più ampio** rispetto alle injection dirette. Le tecniche degli attaccanti evolvono alla stessa velocità dei progressi nelle capacità AI.

---

## 6. Quadro Normativo

Il contesto regolatorio europeo e internazionale sta evolvendo rapidamente in risposta a questi rischi, aggiungendo un livello di obblighi legali all'imperativo di sicurezza.

L'**[EU AI Act](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)** — in vigore dal 2024 con applicazione progressiva fino al 2026 — impone obblighi di trasparenza e documentazione sull'uso dei sistemi AI nei processi aziendali. Il **GDPR** si applica già oggi a qualsiasi trattamento di dati personali attraverso sistemi AI: inviare dati di clienti o dipendenti a modelli cloud senza adeguata base giuridica e Data Processing Agreement firmato costituisce una violazione sanzionabile.

Il **[NIST AI Risk Management Framework](https://www.nist.gov/artificial-intelligence)** e l'**[ISO 42001](https://www.iso.org/standard/81230.html)** stanno diventando riferimenti contrattuali: clienti enterprise e partner commerciali iniziano a richiedere evidenza di governance AI strutturata come prerequisito per le partnership. Un'azienda che non può dimostrare di gestire i propri AI tools con policy documentate e audit trail rischia di essere esclusa da gare e contratti.

---

## 7. La Governance Come Risposta, Non Come Freno

Tutti gli incidenti documentati in questo capitolo condividono una caratteristica comune: **sarebbero stati prevenibili** con policy chiare, configurazioni con privilegio minimo e un processo di review del codice AI-generato.

>[!IMPORTANT]
>Non si tratta di vietare gli strumenti AI — sarebbe controproducente e, come mostrano i dati sulla Shadow AI, inefficace. Si tratta di adottarli come si adotta qualsiasi tecnologia critica: con una valutazione del rischio, una policy d'uso, una configurazione enterprise e un training adeguato del team.

Le organizzazioni che hanno policy di governance AI attive e audit regolari mostrano costi di breach significativamente inferiori e — fatto ancora più rilevante — una **capacità di recupero post-incidente drasticamente più rapida**. Il [dato IBM 2025](https://newsroom.ibm.com/2025-07-30-ibm-report-13-of-organizations-reported-breaches-of-ai-models-or-applications,-97-of-which-reported-lacking-proper-ai-access-controls) mostra che la maggior parte delle organizzazioni senza governance impiega oltre 100 giorni per riprendersi da una violazione.

Nelle sezioni successive, questo documento costruirà il framework di adozione che permette al team di catturare i benefici reali e misurabili degli AI agent — produttività, qualità, velocità di delivery — con il livello di controllo che il contesto enterprise richiede.

---

### Riepilogo dei rischi documentati in questo capitolo

| Rischio | Evidenza | Impatto |
|---|---|---|
| Shadow AI non governata | [49% dev usa tool non approvati — CSO Online 2025](https://www.csoonline.com/article/4111384/top-5-real-world-ai-security-threats-revealed-in-2025.html) | Esposizione dati, violazioni GDPR |
| Codice AI intrinsecamente insicuro | [45% scelta metodo insicuro — Veracode 2025](https://blog.barrack.ai/every-ai-app-data-breach-2025-2026/) | Vulnerabilità in produzione |
| Prompt Injection su AI Agent | [#1 OWASP LLM Top 10, 73% deployment vulnerabili](https://www.obsidiansecurity.com/blog/prompt-injection) | Furto credenziali, esecuzione codice malevolo |
| MCP supply chain attacks | [CVE-2025-6514, 437K+ ambienti esposti](https://authzed.com/blog/timeline-mcp-breaches) | RCE su macchine developer |
| Permessi eccessivi degli agenti | [97% organizzazioni violate senza access control AI — IBM 2025](https://newsroom.ibm.com/2025-07-30-ibm-report-13-of-organizations-reported-breaches-of-ai-models-or-applications,-97-of-which-reported-lacking-proper-ai-access-controls) | Esfiltrazione dati a cascata |
| Shadow AI breach cost premium | [+$670K per breach da Shadow AI — IBM 2025](https://newsroom.ibm.com/2025-07-30-ibm-report-13-of-organizations-reported-breaches-of-ai-models-or-applications,-97-of-which-reported-lacking-proper-ai-access-controls) | Danno economico diretto |
| Assenza governance post-breach | [Recupero >100 giorni senza policy — IBM 2025](https://newsroom.ibm.com/2025-07-30-ibm-report-13-of-organizations-reported-breaches-of-ai-models-or-applications,-97-of-which-reported-lacking-proper-ai-access-controls) | Disruption operativa prolungata |
