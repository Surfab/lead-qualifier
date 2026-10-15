# Changelog

[🇮🇹 Italiano](#italiano) · [🇬🇧 English](#english)

---

## Italiano

### lead-qualifier 1.1.0 (2026-10-15), prima versione pubblica

Cambiamenti rispetto alla 1.0, usata in privato:

- **Regola del verdetto univoca.** ❌ conta per la soglia di REJECT, ⚠️ no ma impedisce l'APPROVE. Aggiunta una tabella di decisione completa, con il criterio di APPROVE che prima non era scritto.
- **Step 0, controllo di ambito.** I lead fuori calibrazione (PMI B2B, studi professionali) vengono segnalati invece di essere respinti in automatico.
- **La reputazione pesa sul verdetto.** Segnali critici da fonti terze portano a REJECT, segnali minori al massimo a RISERVA. Aggiunte query in italiano.
- **Twitter/X sotto soglia.** Un profilo attivo con meno di 10k follower ora è ⚠️ (prima il caso non era coperto).
- **Soglia dichiarata.** L'output riporta sempre "Soglia applicata" e la riga della tabella che è scattata.
- **Uso responsabile.** Nuova sezione su dati pubblici e pertinenza.
- **Esempio fittizio.** Il caso reale è stato sostituito da un lead inventato.
- **Testo indipendente dall'agente.** Nessun riferimento a uno strumento di ricerca specifico o all'autore.
- **plugin.json.** Descrizione completa (era troncata), versione, autore, licenza e parole chiave.

---

## English

### lead-qualifier 1.1.0 (2026-10-15), first public release

Changes from 1.0, which was used privately:

- **Unambiguous verdict rule.** ❌ counts toward the REJECT threshold. ⚠️ does not, but it blocks APPROVE. Added a complete decision table, including the APPROVE criterion that was never written down before.
- **Step 0, scope check.** Leads outside the calibrated scope (B2B SMEs, professional firms) are flagged instead of being rejected automatically.
- **Reputation affects the verdict.** Critical third-party signals lead to REJECT, minor signals cap the verdict at RISERVA. Added Italian-language search queries.
- **Twitter/X below threshold.** An active profile with fewer than 10k followers is now ⚠️ (the case was not covered before).
- **Declared threshold.** The output always reports the threshold applied and the decision-table row that fired.
- **Responsible use.** New section on public, relevant data.
- **Fictional example.** The real-person example was replaced with an invented lead.
- **Agent-independent text.** No references to a specific search tool or to the author.
- **plugin.json.** Full description (it was truncated), version, author, license and keywords.
