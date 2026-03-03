# ⚠️ Il Rischio dell'Adozione Non Governata degli AI Agent

[Torna all'indice](../README.md) · [Prossimo: Trend di Mercato →](01-market-trends.md)

## INTRODUZIONE

Gli AI Agent per lo sviluppo software — Claude Code, GitHub Copilot, Cursor e strumenti analoghi — sono oggi tra le tecnologie più trasformative a disposizione di un team di sviluppo. Promettono, e in molti casi mantengono, guadagni di produttività straordinari: task che richiedevano giorni si comprimono in ore, la curva di apprendimento su nuove tecnologie si appiattisce ed i bug possono essere intercettati prima.

Ma questi strumenti portano con sé una caratteristica unica rispetto a qualsiasi software adottato in precedenza: **agiscono** e **generano** contenuto in base al contesto di lavoro. Non si limitano a rispondere a domande. Leggono il codebase, eseguono comandi, accedono a repository, interrogano database, invocano API. Operano con i **privilegi del developer che li ha configurati**. Molte volte questa caratteristica non viene correttamente considerata e potrebbe essere rischiosa tanto quanto vantaggiosa.

Un aspetto sottovalutato o ignorato nelle organizzazioni è che il team **sta già usando** strumenti AI, approvati o meno. Github copilot è già presente su VSCode e basta un collegamento internet per l'utilizzo di Claude Code di Anthropic o ChatGPT di OpenAI.

Sia per curiosità, per cultura personale o per divertimento, tecnici e ingenieri vengono tentati all'utilizzo di questi strumenti anche in ambiente lavorativo senza una corretta informazione dei rischi.

### Quindi?

Questo documento non ha lo scopo di scoraggiare l'adozione, i vantaggi sono reali e sostanziali (come illustrato nelle sezioni successive). 

Quindi gli obiettivi di questo documento sono due: 
1. fornire un quadro onesto dei rischi, affinché le decisioni di adozione siano informate e ci siano gli elementi per costruire una governance proporzionata alla posta in gioco.

2. cercare di creare le basi affinchè l'utilizzo di queste tecnologie possano trarre vantaggi tangibili alla azienda ed alla buona riuscita delle azioni produttive.

Questi intenti non sono semplici tenendo conto que queste sono tecnologie in costante evoluzione.

### Route map

a. Stabilire delle aree di utilizzo con piccoli esempi

b. Individuare le aree di rischio e contenimento (best practises)

c. Confrontare un tool di codebase generativo rispetto ad un altro di co-working

d. Breve guida alle modalità di utilizzo (system prompt, prompt, context config files, ecc.)

e. Conclusioni finali



---

*[Torna all'indice](../README.md) · [Prossimo: Trend di Mercato →](01-market-trends.md)*
