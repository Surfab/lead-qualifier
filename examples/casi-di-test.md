# Casi di test / Test cases: lead-qualifier

[🇮🇹 Italiano](#italiano) · [🇬🇧 English](#english)

---

## Italiano

Sei lead fittizi, uno per ogni riga della tabella di decisione più il controllo di ambito. Servono a verificare che una modifica alla skill non cambi i verdetti attesi: dai all'agente lo scenario, confronta il verdetto con la colonna "Atteso".

| # | Scenario | Twitter/X | YouTube | Trustpilot | Reputazione | Atteso | Perché |
|---|---|---|---|---|---|---|---|
| 1 | Creator con corso online, community attiva | ✅ 85k, attivo | ✅ 210k, settimanale | ✅ 4.4 su 900 recensioni | Nessun segnale | **APPROVE** | 0 ❌, 0 ⚠️, reputazione pulita |
| 2 | Holding B2B di un founder noto | ✅ 300k, attivo | ✅ 90k, mensile | ⚠️ non applicabile (B2B) | Nessun segnale | **RISERVA** | 0 ❌ ma un ⚠️ impedisce l'APPROVE |
| 3 | Consulente con canale video forte | ❌ inattivo da 14 mesi | ✅ 60k, settimanale | ⚠️ non applicabile | Nessun segnale | **RISERVA** | 1 ❌, sotto la soglia di 2 |
| 4 | E-commerce di integratori | ✅ 20k, attivo | ❌ assente | ❌ 2.1, lamentele su rimborsi | Non si verifica | **REJECT** | 2 ❌, scatta la regola, Step 3 saltato |
| 5 | Info-marketer con numeri alti | ✅ 150k, attivo | ✅ 400k, settimanale | ✅ 3.8 | Segnali critici: inchiesta di una testata su rimborsi negati | **REJECT** | Segnali critici da fonte terza battono i canali positivi |
| 6 | PMI manifatturiera B2B senza social | ❌ assente | ❌ assente | ⚠️ non applicabile | n/d | **Fuori calibrazione** | Step 0: chiedere all'utente prima di applicare la regola |

### Cosa guardare oltre al verdetto

- La tabella canali arriva prima di qualsiasi testo narrativo.
- Ogni numero ha una fonte, e i dati auto-dichiarati sono marcati come tali.
- Il blocco verdetto riporta "Soglia applicata" e la riga della tabella di decisione che è scattata.
- C'è sempre un next step di una riga.

---

## English

Six fictional leads, one for each row of the decision table plus the scope check. Use them to verify that a change to the skill does not change the expected verdicts: give the agent the scenario and compare its verdict with the "Expected" column.

| # | Scenario | Twitter/X | YouTube | Trustpilot | Reputation | Expected | Why |
|---|---|---|---|---|---|---|---|
| 1 | Creator with an online course and an active community | ✅ 85k, active | ✅ 210k, weekly | ✅ 4.4 from 900 reviews | No signals | **APPROVE** | 0 ❌, 0 ⚠️, clean reputation |
| 2 | B2B holding of a well-known founder | ✅ 300k, active | ✅ 90k, monthly | ⚠️ not applicable (B2B) | No signals | **RISERVA** | 0 ❌, but one ⚠️ blocks APPROVE |
| 3 | Consultant with a strong video channel | ❌ inactive for 14 months | ✅ 60k, weekly | ⚠️ not applicable | No signals | **RISERVA** | 1 ❌, below the threshold of 2 |
| 4 | Supplements e-commerce | ✅ 20k, active | ❌ missing | ❌ 2.1, refund complaints | Not checked | **REJECT** | 2 ❌, rule triggered, Step 3 skipped |
| 5 | Info-marketer with big numbers | ✅ 150k, active | ✅ 400k, weekly | ✅ 3.8 | Critical signals: press investigation into denied refunds | **REJECT** | Critical third-party signals outweigh positive channels |
| 6 | B2B manufacturing SME with no social media | ❌ missing | ❌ missing | ⚠️ not applicable | n/a | **Out of scope** | Step 0: ask the user before applying the rule |

### What to check beyond the verdict

- The channel table comes before any narrative text.
- Every number has a source, and self-reported data is marked as such.
- The verdict block shows "Soglia applicata" (threshold applied) and the decision-table row that fired.
- There is always a one-line next step.
