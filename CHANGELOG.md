# Changelog

[🇮🇹 Italiano](#italiano) · [🇬🇧 English](#english)

---

## Italiano

### lead-qualifier 1.2.0 (2026-10-15)

- **Nuova skill lead-qualifier-studi 1.0.0.** Variante per professionisti iscritti a un Ordine e studi professionali. Canali: LinkedIn, Albo/Ordine, pubblicazioni ed eventi, con disambiguazione degli omonimi.
- **Rispetto alla versione privata di lead-qualifier-studi:** tabella di decisione ordinata (vale la prima riga), reputazione che pesa sul verdetto, Albo ⚠️ distinto da ❌ (albo non consultabile contro iscrizione non trovata), contenzioso considerato solo quando lo studio è parte in causa, esempio fittizio, testo indipendente dall'autore e dallo strumento di ricerca.
- **lead-qualifier 1.2.0.** Lo Step 0 rimanda a lead-qualifier-studi quando il lead è un professionista iscritto a un Ordine.
- **Casi di test.** Otto casi per lead-qualifier-studi. Per lead-qualifier aggiunti il caso dei segnali minori, che mancava, e quello del passaggio a lead-qualifier-studi.

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

### lead-qualifier 1.2.0 (2026-10-15)

- **New skill: lead-qualifier-studi 1.0.0.** A variant for members of professional bodies (Ordini) and professional firms. Channels: LinkedIn, professional register (Albo/Ordine), publications and events, with disambiguation of people with the same name.
- **Compared with the private version of lead-qualifier-studi:** ordered decision table (the first matching row wins), reputation affects the verdict, register ⚠️ separated from ❌ (register unavailable versus membership not found), litigation counted only when the firm itself is a party, fictional example, text independent of the author and of the search tool.
- **lead-qualifier 1.2.0.** Step 0 hands over to lead-qualifier-studi when the lead is a member of a professional body.
- **Test cases.** Eight cases for lead-qualifier-studi. For lead-qualifier, added the missing minor-signals case and the hand-over case.

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
