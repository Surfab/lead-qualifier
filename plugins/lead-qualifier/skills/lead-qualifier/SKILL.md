---
name: lead-qualifier
description: Qualifica un potenziale cliente (lead) prima del primo contatto commerciale. Verifica la presenza pubblica su tre canali obbligatori (social principale tra X, Instagram, TikTok e LinkedIn, poi YouTube e Trustpilot), controlla la reputazione online e restituisce un verdetto APPROVE, RISERVA o REJECT con fonti e un next step. Usala quando l'utente chiede di analizzare un potenziale cliente, valutare un lead o verificare una persona o un'azienda prima di contattarla, per esempio "valuta questo lead" o "controlla [nome] prima che lo contatti". Also use it when the user asks in English to qualify a lead, vet a prospect or check a person or company before sales outreach, for example "qualify this lead" or "is this prospect worth contacting". Non usarla per ricerche generiche su persone o aziende senza un contesto commerciale.
license: MIT
metadata:
  author: Fabrizio Quaglio Cotti
  version: "1.3.0"
---

# Lead Qualifier

Decide se vale la pena contattare un lead prima di investirci tempo. Cerca il lead su tre canali pubblici, applica una regola di squalifica esplicita e chiude con un verdetto motivato.

---

## 1. Obiettivo

Dato il nome di una persona o di un'azienda, verifica presenza pubblica, credibilità e reputazione, e produce uno di tre verdetti: **APPROVE**, **RISERVA** o **REJECT**.

La regola centrale:

> **Se i canali obbligatori ❌ (assenti o con segnali negativi) raggiungono la soglia, il verdetto è REJECT immediato. Nessuna eccezione. La soglia di default è 2.**

### Stati dei canali

| Stato | Significato | Conta per il REJECT? |
|---|---|---|
| ✅ | Presente, attivo, coerente con il posizionamento | No |
| ⚠️ | Non applicabile al tipo di business, presenza debole o dato non verificabile | No, ma impedisce l'APPROVE |
| ❌ | Assente quando dovrebbe esserci, abbandonato o con segnali negativi | Sì |

### Tabella di decisione

Applica la prima riga che corrisponde. S è la soglia (default 2).

| Canali ❌ | Canali ⚠️ | Reputazione (Step 3) | Verdetto |
|---|---|---|---|
| S o più | qualsiasi | non si verifica | **REJECT** |
| meno di S | qualsiasi | segnali critici | **REJECT** |
| almeno 1, meno di S | qualsiasi | nessun segnale critico | **RISERVA** |
| 0 | 1 o più | nessun segnale critico | **RISERVA** |
| 0 | 0 | segnali minori | **RISERVA** |
| 0 | 0 | nessun segnale negativo | **APPROVE** |

Con la soglia di default (S = 2) le righe si leggono così: 2 o più ❌ → REJECT; 1 ❌ → RISERVA, salvo segnali critici.

La soglia si può cambiare solo prima dell'analisi, su richiesta dell'utente (per esempio S = 1 per un filtro più severo, S = 3 per uno più largo). Va dichiarata nell'output ("Soglia applicata") e non si reinterpreta durante l'analisi.

---

## 2. Tono

- Diretto, senza preamboli.
- Dati prima, interpretazioni dopo. Ogni numero ha una fonte.
- Nessun entusiasmo artificiale. Se il lead è debole, lo dici.
- Tabelle e verdetto prima di qualsiasi analisi narrativa.
- Italiano, professionale ma colloquiale.

---

## 3. Processo

### Step 0. Verifica l'ambito

La regola dei canali è calibrata su creator, founder, personal brand e aziende con un pubblico consumer. Su PMI B2B, studi professionali o aziende senza canali social produce REJECT falsi.

Se il lead è un professionista iscritto a un Ordine (commercialista, avvocato, notaio, consulente del lavoro) o uno studio professionale, usa la skill `lead-qualifier-studi`, che misura i canali giusti per quel segmento.

Per gli altri casi fuori calibrazione:
- se puoi, chiedi all'utente se procedere comunque;
- se non puoi, procedi e scrivi in testa all'output: "Ambito: fuori calibrazione. Verdetto indicativo."

### Step 1. Cerca sui tre canali obbligatori

Fai sempre tutte e tre le ricerche con lo strumento di ricerca web disponibile. Non saltarne nessuna, anche se il lead sembra ovviamente positivo o negativo. Non usare dati memorizzati e non dare per scontato che un profilo esista.

**Social principale**
- Cerca il lead su X, Instagram, TikTok e LinkedIn. Il social principale è quello con più follower attivi: valuta solo quello e cita gli altri come segnale in più.
- Query: `[nome] Instagram`, `[nome] TikTok`, `[nome] LinkedIn`, `[nome] X.com`
- Verifica: profilo, follower, frequenza di pubblicazione, tono
- ✅ profilo attivo, oltre 10k follower, contenuti coerenti con il posizionamento dichiarato
- ⚠️ profilo attivo ma sotto i 10k follower, oppure dati non verificabili
- ❌ nessun profilo sui quattro social, oppure tutti inattivi da oltre 6 mesi, oppure contenuti spam o controversi sul social principale
- Un founder B2B attivo solo su LinkedIn ha un social principale valido: non serve che sia anche su X.

**YouTube**
- Query: `[nome] YouTube channel`
- Verifica: canale, iscritti, frequenza di upload
- ✅ canale attivo, oltre 1.000 iscritti, contenuti coerenti
- ⚠️ canale attivo ma sotto i 1.000 iscritti o con upload irregolari, oppure canale assente in un business dove il video non è un canale atteso (vedi Sezione 6)
- ❌ canale abbandonato da oltre 6 mesi, commenti negativi sistematici, oppure canale assente in un business dove il video è atteso

**Trustpilot**
- Query: `[nome] OR [azienda] Trustpilot`
- Verifica: pagina, punteggio, numero di recensioni, pattern di lamentele
- ✅ punteggio di almeno 3.0, recensioni coerenti
- ❌ punteggio sotto 3.0, lamentele ricorrenti su frodi, mancati pagamenti, sparizioni
- Pagina assente: classifica in base al tipo di business (vedi Sezione 6)

### Step 2. Applica la regola di squalifica

Conta i canali ❌ e quelli ⚠️. Se i ❌ raggiungono la soglia (default 2), emetti **REJECT** subito, salta Step 3 e 4 e vai all'output.

### Step 3. Ricerca reputazionale allargata

Solo se non c'è già un REJECT.

- Query: `[nome] controversy OR scam OR complaints OR negative reviews`, senza filtro di data: le truffe più documentate sono spesso vecchie
- Ripeti la stessa query con l'anno corrente per i segnali recenti
- Query: `[nome] [azienda principale] criticism`
- Per lead italiani: `[nome] truffa OR lamentele OR recensioni negative`
- Verifica Reddit, Hacker News e i forum di settore

Classifica il risultato:
- **Segnali critici**: frodi, truffe, mancati pagamenti o cause per pratiche scorrette, documentati da fonti terze attendibili
- **Segnali minori**: critiche isolate, polemiche senza conseguenze, lamentele sporadiche
- **Nessun segnale negativo**: va scritto esplicitamente, è un dato

Poi applica la tabella di decisione.

### Step 4. Profilo commerciale

**Identità verificabile**
- Ruolo attuale e azienda principale
- Exit o acquisizioni confermate da fonti terze (TechCrunch, Business Insider, Crunchbase), non solo auto-dichiarate
- Background professionale e area geografica

**Numeri pubblici**
- Follower totali sui canali attivi
- Fatturato, se disponibile da fonti attendibili
- Dimensione del team

**Posizionamento**
- Pubblico servito, prodotti o servizi attivi
- Collocazione nel mercato: B2B, B2C, educator, founder, investor, agenzia

**Segnali di rischio**
- Dipendenza eccessiva dalla persona (personal brand puro contro azienda strutturata)
- Exit con termini non verificabili o legate ad aziende poi fallite
- Distanza tra come il lead si racconta e cosa dicono le fonti esterne

### Step 5. Output

Produci nell'ordine:
1. Riga di ambito, solo se lo Step 0 l'ha richiesta
2. Tabella canali
3. Tabella profilo commerciale
4. Verdetto con motivazione
5. Next step concreto (una riga)

---

## 4. Da fare e da evitare

**Da fare**
- Cerca sempre tutti e tre i canali, anche quando il verdetto sembra già chiaro.
- Classifica Trustpilot e YouTube come ⚠️ quando il tipo di business non li prevede, e spiega perché.
- Cita la fonte di ogni dato rilevante: follower, acquisizioni, fatturato.
- Emetti REJECT senza attenuanti quando scatta la regola. Niente "però ha punti positivi".
- Registra l'assenza di segnali negativi. "Nessun risultato negativo trovato" è un dato, non un vuoto.
- Chiudi sempre con un next step concreto: canale di contatto, momento, angolo da usare.

**Da evitare**
- Non gonfiare i segnali positivi per compensare quelli mancanti. Due canali forti e Trustpilot assente restano un lead con un canale mancante.
- Non reinterpretare la soglia durante l'analisi.
- Non confondere ⚠️ con ✅.
- Non presentare dati auto-dichiarati come verificati. "Il lead dichiara un fatturato a otto cifre" non vale quanto "una fonte terza riporta X".
- Non scrivere analisi narrative prima del verdetto.
- Non usare aggettivi generici ("impressionante", "solido", "notevole"). Usa i numeri.

---

## 5. Uso responsabile

- Usa solo informazioni pubbliche e pertinenti a una decisione commerciale.
- Non raccogliere dati personali estranei al business: famiglia, salute, opinioni politiche o religiose, indirizzo privato.
- Il verdetto dice se investire tempo in un contatto. Non è un giudizio sulla persona.
- Nel primo contatto, chi usa la skill deve dire al lead da dove ha preso i suoi dati (GDPR, art. 14). La base giuridica tipica è il legittimo interesse.

---

## 6. Gestione delle fonti

### Trustpilot o YouTube assenti

Non sono automaticamente un segnale negativo. Dipende dal tipo di business:

| Tipo di business | Trustpilot assente | YouTube assente |
|---|---|---|
| E-commerce, SaaS consumer, servizi al consumatore | ❌ Segnale negativo | ❌ Segnale negativo |
| Creator o educator che vende corsi, community o infoprodotti | ⚠️ Non applicabile, ma cerca recensioni del corso su Google, Udemy o Skool: lamentele ricorrenti lì valgono ❌ | ❌ Segnale negativo |
| Agenzia B2B, holding, consulente, founder B2B | ⚠️ Non applicabile | ⚠️ Non applicabile |
| Personal brand senza prodotti venduti al pubblico | ⚠️ Non applicabile | ⚠️ Non applicabile se il social principale è ✅, altrimenti ❌ |
| Startup early stage | ⚠️ Non applicabile, troppo presto | ⚠️ Non applicabile, troppo presto |

In ogni caso segnala l'assenza e spiega la classificazione scelta.

### Fonti con paywall

Se un articolo richiede login, usa il dato visibile nello snippet e segnala che la fonte è accessibile solo in parte. Non inventare dati per completare la scheda. Scrivi: "Dato non verificabile da fonti pubbliche."

Per acquisizioni con termini non divulgati: l'evento è verificato, i valori economici no.

### Dati auto-dichiarati

Tieni separati i dati dichiarati dal lead da quelli confermati da fonti indipendenti:
- "Dichiara X" (fonte: video o post del lead)
- "Confermato da TechCrunch: acquisizione avvenuta, termini non divulgati"

Non presentarli con lo stesso livello di affidabilità.

### Social inaccessibile

Se la pagina non si carica (succede spesso con Instagram, LinkedIn e X senza login):
- usa gli snippet dei risultati di ricerca;
- cerca dati aggregati su SocialBlade o Viewstats;
- cerca `[nome] [social] followers [anno]` per fonti secondarie.

Se nessuna fonte è disponibile, classifica come ⚠️ con la nota "dati follower non verificabili direttamente".

---

## Template di output

### Tabella canali

| Canale | Stato | Dettaglio |
|---|---|---|
| Social principale ([quale]) | ✅ / ⚠️ / ❌ | Follower, frequenza, fonte. Altri social attivi tra parentesi |
| YouTube | ✅ / ⚠️ / ❌ | Iscritti, frequenza, fonte |
| Trustpilot | ✅ / ⚠️ / ❌ | Punteggio, recensioni, o motivo dell'assenza |

Legenda: ✅ positivo · ⚠️ non applicabile, debole o incerto · ❌ assente o negativo

### Tabella profilo commerciale

| Aspetto | Segnale |
|---|---|
| Credibilità pubblica | Alta / Media / Bassa |
| Business reale e verificabile | Sì / No / Parziale |
| Reputazione | Nessun segnale negativo / Segnali minori / Segnali critici |
| Tipo di cliente | es. educator, founder, corporate, agenzia |
| Budget probabile | stima di range |
| Rischio principale | descrizione sintetica |

### Verdetto

```text
VERDETTO: [APPROVE / RISERVA / REJECT]

Motivazione: [1-2 righe]

Canali ❌: [n su 3] · Canali ⚠️: [n su 3]
Soglia applicata: [S, default 2]
Regola scattata: [riga della tabella di decisione, oppure "nessuna"]
```

**Next step:** [Una riga. Canale di contatto, angolo da usare, o azione da completare prima di procedere.]

---

## Esempio completo (lead fittizio, dati inventati)

Lead: Acme Academy, società che vende formazione AI a team aziendali.

| Canale | Stato | Dettaglio |
|---|---|---|
| Social principale (X) | ✅ | 48k follower su @acme_esempio, 1-2 post al giorno (fonte: x.com). Attiva anche su LinkedIn |
| YouTube | ✅ | 120k iscritti, 2 video a settimana negli ultimi 6 mesi (fonte: youtube.com) |
| Trustpilot | ⚠️ | Pagina assente. Acme vende a team aziendali (B2B) e non genera recensioni consumer |

| Aspetto | Segnale |
|---|---|
| Credibilità pubblica | Alta |
| Business reale e verificabile | Sì. Clienti aziendali citati in due case study di terze parti |
| Reputazione | Nessun segnale negativo trovato (query in inglese e in italiano) |
| Tipo di cliente | Founder + educator |
| Budget probabile | Mid-market |
| Rischio principale | Business molto legato alla founder; fatturato solo auto-dichiarato |

```text
VERDETTO: RISERVA

Motivazione: Nessun canale ❌, un canale ⚠️ (Trustpilot non applicabile al modello B2B).
Nessun segnale negativo. Lead attivo, da approcciare con una proposta mirata.

Canali ❌: 0 su 3 · Canali ⚠️: 1 su 3
Soglia applicata: 2
Regola scattata: 0 ❌ e 1 o più ⚠️ → RISERVA
```

**Next step:** Contatto via X (@acme_esempio) dopo aver scelto un angolo preciso, per esempio l'automazione dei materiali dei corsi per i team clienti. Non un pitch generico.
