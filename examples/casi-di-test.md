# Casi di test / Test cases

[🇮🇹 Italiano](#italiano) · [🇬🇧 English](#english)

---

## Italiano

Lead fittizi, uno per ogni riga delle tabelle di decisione. Servono a verificare che una modifica alle skill non cambi i verdetti attesi: dai all'agente lo scenario, confronta il verdetto con la colonna "Atteso".

### lead-qualifier

Nove casi: uno per ogni riga della tabella, i due controlli di ambito dello Step 0 e quello del founder B2B attivo solo su LinkedIn.

| # | Scenario | Social principale | YouTube | Trustpilot | Reputazione | Atteso | Perché |
|---|---|---|---|---|---|---|---|
| 1 | Creator con corso online, community attiva | ✅ Instagram 85k, attivo | ✅ 210k, settimanale | ✅ 4.4 su 900 recensioni | Nessun segnale | **APPROVE** | 0 ❌, 0 ⚠️, reputazione pulita |
| 2 | Holding B2B di un founder noto | ✅ 300k, attivo | ✅ 90k, mensile | ⚠️ non applicabile (B2B) | Nessun segnale | **RISERVA** | 0 ❌ ma un ⚠️ impedisce l'APPROVE |
| 3 | Consulente con canale video forte | ❌ X inattivo da 14 mesi, nessun altro social attivo | ✅ 60k, settimanale | ⚠️ non applicabile | Nessun segnale | **RISERVA** | 1 ❌, sotto la soglia di 2 |
| 4 | E-commerce di integratori | ✅ 20k, attivo | ❌ assente | ❌ 2.1, lamentele su rimborsi | Non si verifica | **REJECT** | 2 ❌, scatta la regola, Step 3 saltato |
| 5 | Info-marketer con numeri alti | ✅ 150k, attivo | ✅ 400k, settimanale | ✅ 3.8 | Segnali critici: inchiesta di una testata su rimborsi negati | **REJECT** | Segnali critici da fonte terza battono i canali positivi |
| 6 | Coach con community a pagamento | ✅ 40k, attivo | ✅ 75k, settimanale | ✅ 4.1 | Segnali minori: un thread Reddit isolato critica i prezzi | **RISERVA** | 0 ❌, 0 ⚠️, ma segnali minori |
| 7 | PMI manifatturiera B2B senza social | ❌ assente | ❌ assente | ⚠️ non applicabile | n/d | **Fuori calibrazione** | Step 0: chiedere all'utente prima di applicare la regola |
| 8 | Studio associato di commercialisti | ❌ assente | ❌ assente | ⚠️ non applicabile | n/d | **Passa a lead-qualifier-studi** | Step 0: il segmento ha una skill dedicata |
| 9 | Founder di un SaaS B2B, attivo solo su LinkedIn | ✅ LinkedIn 25k, attivo. Assente su X | ⚠️ assente, video non atteso per un SaaS B2B | ⚠️ non applicabile (B2B) | Nessun segnale | **RISERVA** | 0 ❌ e 2 ⚠️. Prima della 1.3.0 era REJECT per l'assenza su X e YouTube |

### lead-qualifier-studi

Dieci casi: uno per ogni riga della tabella, più quello che distingue questa variante dalla base (un solo ⚠️ non blocca l'APPROVE), quello del piccolo studio con Albo verificato e quello del LinkedIn trovato ma non leggibile.

| # | Scenario | LinkedIn | Albo / Ordine | Pubblicazioni ed eventi | Reputazione | Atteso | Perché |
|---|---|---|---|---|---|---|---|
| 1 | Avvocato con forte presenza online | ✅ profilo attivo | ❌ sanzione disciplinare pubblica | ✅ docenze recenti | Non si verifica | **REJECT** | Albo ❌ batte tutto il resto |
| 2 | Studio senza presenza online e albo non consultabile | ❌ né profilo né pagina | ⚠️ iscrizione dichiarata solo dal sito dello studio | ❌ nessuna traccia | Non si verifica | **REJECT** | 2 ❌ e Albo ⚠️ |
| 3 | Notaio con canali in ordine | ✅ profilo attivo | ✅ iscrizione verificata | ✅ articoli recenti | Segnali critici: inchiesta di stampa su un procedimento che riguarda lo studio | **REJECT** | Segnali critici da fonte terza |
| 4 | Commercialista senza pubblicazioni | ✅ profilo attivo | ✅ iscrizione verificata | ❌ nessuna traccia | Nessun segnale | **RISERVA** | 1 ❌ |
| 5 | Consulente del lavoro | ⚠️ profilo fermo da 2 anni | ✅ iscrizione verificata | ⚠️ ultimo intervento nel 2019 | Nessun segnale | **RISERVA** | 0 ❌ e 2 ⚠️ |
| 6 | Studio di consulenza fiscale | ✅ pagina e profili attivi | ✅ iscrizione verificata | ✅ convegno nel 2025 | Segnali minori: due recensioni negative isolate | **RISERVA** | Segnali minori |
| 7 | Avvocata socia di uno studio d'affari | ✅ profilo attivo | ✅ iscrizione verificata | ✅ relatrice a un convegno nel 2025 | Nessun segnale | **APPROVE** | 0 ❌, 0 ⚠️ |
| 8 | Commercialista in studio associato | ⚠️ solo pagina dello studio | ✅ iscrizione verificata | ✅ articolo su rivista di settore, 2024 | Nessun segnale | **APPROVE** | 0 ❌ e un solo ⚠️, che qui non blocca l'APPROVE |
| 9 | Piccolo studio di provincia senza presenza online | ❌ né profilo né pagina | ✅ iscrizione verificata | ❌ nessuna traccia | Nessun segnale | **RISERVA** | 2 ❌ ma Albo ✅: l'iscrizione verificata pesa più della visibilità. Contatto via email o telefono dello studio |
| 10 | Avvocato con LinkedIn dietro login | ⚠️ profilo presente negli snippet ma non leggibile senza login | ✅ iscrizione verificata | ✅ docenza nel 2025 | Nessun segnale | **APPROVE** | Non leggibile vale ⚠️, non ❌. 0 ❌ e un solo ⚠️ |

### Cosa guardare oltre al verdetto

- La tabella canali arriva prima di qualsiasi testo narrativo.
- Ogni numero ha una fonte, e i dati auto-dichiarati sono marcati come tali.
- Il blocco verdetto riporta la riga della tabella di decisione che è scattata (e in lead-qualifier anche "Soglia applicata").
- In lead-qualifier-studi c'è sempre la riga degli omonimi scartati.
- In lead-qualifier-studi l'output si apre con la riga "Sintesi", gli stati sono solo ✅, ⚠️ e ❌, i valori della tabella profilo sono quelli fissi del template, e se l'Albo è ⚠️ c'è il link per verificarlo a mano. Se l'Albo ✅ cambierebbe il verdetto, l'agente chiede la verifica prima di chiudere oppure riporta entrambi i verdetti.
- Gli omonimi scartati sono descritti solo con professione e città. Se l'utente conosce già il lead, c'è la riga "Relazione esistente" dopo la sintesi e il next step è un contatto diretto. Il testo narrativo sta nelle Note, dopo il next step.
- Nessun aggregatore o directory è usato come fonte per il ✅ dell'Albo.
- C'è sempre un next step di una riga.

---

## English

Fictional leads, one for each row of the decision tables. Use them to verify that a change to the skills does not change the expected verdicts: give the agent the scenario and compare its verdict with the "Expected" column.

### lead-qualifier

Nine cases: one for each row of the table, the two Step 0 scope checks, and the B2B founder who is active only on LinkedIn.

| # | Scenario | Main social | YouTube | Trustpilot | Reputation | Expected | Why |
|---|---|---|---|---|---|---|---|
| 1 | Creator with an online course and an active community | ✅ Instagram 85k, active | ✅ 210k, weekly | ✅ 4.4 from 900 reviews | No signals | **APPROVE** | 0 ❌, 0 ⚠️, clean reputation |
| 2 | B2B holding of a well-known founder | ✅ 300k, active | ✅ 90k, monthly | ⚠️ not applicable (B2B) | No signals | **RISERVA** | 0 ❌, but one ⚠️ blocks APPROVE |
| 3 | Consultant with a strong video channel | ❌ X inactive for 14 months, no other active social | ✅ 60k, weekly | ⚠️ not applicable | No signals | **RISERVA** | 1 ❌, below the threshold of 2 |
| 4 | Supplements e-commerce | ✅ 20k, active | ❌ missing | ❌ 2.1, refund complaints | Not checked | **REJECT** | 2 ❌, rule triggered, Step 3 skipped |
| 5 | Info-marketer with big numbers | ✅ 150k, active | ✅ 400k, weekly | ✅ 3.8 | Critical signals: press investigation into denied refunds | **REJECT** | Critical third-party signals outweigh positive channels |
| 6 | Coach with a paid community | ✅ 40k, active | ✅ 75k, weekly | ✅ 4.1 | Minor signals: one isolated Reddit thread criticises the prices | **RISERVA** | 0 ❌, 0 ⚠️, but minor signals |
| 7 | B2B manufacturing SME with no social media | ❌ missing | ❌ missing | ⚠️ not applicable | n/a | **Out of scope** | Step 0: ask the user before applying the rule |
| 8 | Associated firm of accountants | ❌ missing | ❌ missing | ⚠️ not applicable | n/a | **Hand over to lead-qualifier-studi** | Step 0: the segment has a dedicated skill |
| 9 | Founder of a B2B SaaS, active only on LinkedIn | ✅ LinkedIn 25k, active. Not on X | ⚠️ missing, video not expected for a B2B SaaS | ⚠️ not applicable (B2B) | No signals | **RISERVA** | 0 ❌ and 2 ⚠️. Before 1.3.0 it was REJECT because of no X and no YouTube |

### lead-qualifier-studi

Ten cases: one for each row of the table, plus the one that sets this variant apart from the base skill (a single ⚠️ does not block APPROVE), the small firm with a verified register entry, and the LinkedIn profile that is found but cannot be read.

| # | Scenario | LinkedIn | Register (Albo / Ordine) | Publications and events | Reputation | Expected | Why |
|---|---|---|---|---|---|---|---|
| 1 | Lawyer with a strong online presence | ✅ active profile | ❌ public disciplinary sanction | ✅ recent teaching | Not checked | **REJECT** | Register ❌ overrides everything else |
| 2 | Firm with no online presence and register unavailable | ❌ no profile, no page | ⚠️ membership stated only on the firm's website | ❌ no trace | Not checked | **REJECT** | 2 ❌ and register ⚠️ |
| 3 | Notary with every channel in order | ✅ active profile | ✅ membership verified | ✅ recent articles | Critical signals: press investigation into proceedings involving the firm | **REJECT** | Critical third-party signals |
| 4 | Accountant with no publications | ✅ active profile | ✅ membership verified | ❌ no trace | No signals | **RISERVA** | 1 ❌ |
| 5 | Labour consultant | ⚠️ profile inactive for 2 years | ✅ membership verified | ⚠️ last talk in 2019 | No signals | **RISERVA** | 0 ❌ and 2 ⚠️ |
| 6 | Tax advisory firm | ✅ active page and profiles | ✅ membership verified | ✅ conference in 2025 | Minor signals: two isolated negative reviews | **RISERVA** | Minor signals |
| 7 | Partner at a corporate law firm | ✅ active profile | ✅ membership verified | ✅ conference speaker in 2025 | No signals | **APPROVE** | 0 ❌, 0 ⚠️ |
| 8 | Accountant at an associated firm | ⚠️ firm page only | ✅ membership verified | ✅ trade journal article, 2024 | No signals | **APPROVE** | 0 ❌ and a single ⚠️, which does not block APPROVE here |
| 9 | Small provincial firm with no online presence | ❌ no profile, no page | ✅ membership verified | ❌ no trace | No signals | **RISERVA** | 2 ❌ but register ✅: verified membership outweighs visibility. Contact via the firm's email or phone |
| 10 | Lawyer with LinkedIn behind a login | ⚠️ profile in search snippets but unreadable without login | ✅ membership verified | ✅ teaching in 2025 | No signals | **APPROVE** | Unreadable counts as ⚠️, not ❌. 0 ❌ and a single ⚠️ |

### What to check beyond the verdict

- The channel table comes before any narrative text.
- Every number has a source, and self-reported data is marked as such.
- The verdict block shows the decision-table row that fired (and, in lead-qualifier, "Soglia applicata", the threshold applied).
- lead-qualifier-studi always includes the line listing people with the same name that were ruled out.
- In lead-qualifier-studi the output opens with the "Sintesi" (summary) line, statuses are only ✅, ⚠️ and ❌, the profile table uses the template's fixed values, and when the register is ⚠️ there is a link to check it by hand. If a ✅ register would change the verdict, the agent asks for the check before closing or reports both verdicts.
- Ruled-out namesakes are described only by profession and city. If the user already knows the lead, there is a "Relazione esistente" (existing relationship) line after the summary and the next step is a direct contact. Narrative text goes in the Notes, after the next step.
- No aggregator or directory is used as the source for a ✅ register.
- There is always a one-line next step.
