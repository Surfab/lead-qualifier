# Changelog

[🇮🇹 Italiano](#italiano) · [🇬🇧 English](#english)

---

## Italiano

I titoli indicano la versione del plugin. Le versioni delle singole skill sono nel testo.

### Plugin 1.3.2 (2026-10-30)

lead-qualifier-studi 1.1.2, dopo la seconda prova sullo stesso studio legale:

- **Omonimi senza dati personali.** Solo professione e città, niente nomi completi né altri dettagli su persone estranee al lead.
- **Relazione esistente.** Se l'utente conosce già il lead, l'output lo dice in una riga dopo la sintesi e il next step diventa un contatto diretto. Il verdetto non cambia.
- **Note in fondo.** Il testo narrativo va in una sezione Note facoltativa dopo il next step, mai prima delle tabelle.
- **Albo decisivo.** Se l'Albo ✅ cambierebbe il verdetto, la skill chiede la verifica prima di chiudere, oppure riporta entrambi i verdetti.
- **Aggregatori esclusi.** Directory e siti che ripubblicano dati dell'albo non valgono come fonte istituzionale.

### Plugin 1.3.1 (2026-10-30)

lead-qualifier-studi 1.1.1, dopo una prova su uno studio legale reale:

- **Solo tre stati.** Niente etichette come "❌ (parziale)". Dato non trovato, nemmeno negli snippet, vale ❌. Dato trovato ma non leggibile (login, modulo che non risponde) vale ⚠️.
- **Albo più facile da verificare.** Se l'Ordine territoriale non risponde, la skill prova il registro nazionale della categoria e i PDF pubblicati sul sito dell'Ordine. Se l'Albo resta ⚠️, l'output dà all'utente il link per controllarlo a mano; con la conferma l'Albo diventa ✅ e il verdetto si ricalcola.
- **Valori fissi nella tabella profilo.** Niente valori intermedi come "Media-alta".
- **Riga di sintesi in apertura.** L'output parte con `Sintesi: [VERDETTO]. [motivo]`, poi le tabelle. Il blocco Verdetto completo resta.
- **Casi di test.** Nuovo caso del LinkedIn trovato ma non leggibile.

### Plugin 1.3.0 (2026-10-30)

lead-qualifier 1.3.0:

- **Social principale al posto di Twitter/X.** Il primo canale è il social dove il lead è più attivo tra X, Instagram, TikTok e LinkedIn. Prima un creator attivo solo su Instagram, o un founder B2B attivo solo su LinkedIn, prendeva ❌ e rischiava un REJECT falso.
- **YouTube ha lo stato ⚠️.** Canale piccolo (sotto 1.000 iscritti) o assente in un business dove il video non è atteso. La tabella della Sezione 6 ora copre sia Trustpilot sia YouTube, con una riga per chi vende corsi e infoprodotti.
- **Tabella di decisione scritta in funzione della soglia.** Le righe usano la soglia S invece del numero 2, così cambiare la soglia non le rende contraddittorie. La soglia si fissa prima dell'analisi.
- **Reputazione senza filtro di data.** La query reputazionale gira prima senza anno, poi con l'anno corrente.

lead-qualifier-studi 1.1.0:

- **L'Albo pesa più della visibilità.** Con l'iscrizione verificata, LinkedIn ❌ e pubblicazioni ❌ danno RISERVA e non più REJECT. Il REJECT resta quando manca anche la verifica dell'Albo.
- **Frasi di attivazione in inglese**, come in lead-qualifier.
- **Blocco verdetto uniforme** con quello di lead-qualifier.

Entrambe:

- **Uso responsabile.** Una riga sull'informativa al primo contatto (GDPR, art. 14).
- **Casi di test.** Nuovo caso del founder B2B solo su LinkedIn; nuovo caso del piccolo studio con Albo verificato; caso 2 di lead-qualifier-studi riscritto per la nuova regola.

### Plugin 1.2.1 (2026-10-15)

- **Attivazione anche in inglese.** La descrizione di lead-qualifier include frasi di attivazione in inglese, così la skill parte anche quando l'utente scrive in inglese. Le istruzioni restano in italiano.

### Plugin 1.2.0 (2026-10-15)

- **Nuova skill lead-qualifier-studi 1.0.0.** Variante per professionisti iscritti a un Ordine e studi professionali. Canali: LinkedIn, Albo/Ordine, pubblicazioni ed eventi, con disambiguazione degli omonimi.
- **Rispetto alla versione privata di lead-qualifier-studi:** tabella di decisione ordinata (vale la prima riga), reputazione che pesa sul verdetto, Albo ⚠️ distinto da ❌ (albo non consultabile contro iscrizione non trovata), contenzioso considerato solo quando lo studio è parte in causa, esempio fittizio, testo indipendente dall'autore e dallo strumento di ricerca.
- **lead-qualifier 1.2.0.** Lo Step 0 rimanda a lead-qualifier-studi quando il lead è un professionista iscritto a un Ordine.
- **Casi di test.** Otto casi per lead-qualifier-studi. Per lead-qualifier aggiunti il caso dei segnali minori, che mancava, e quello del passaggio a lead-qualifier-studi.

### Plugin 1.1.0 (2026-10-15), prima versione pubblica

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

Headings show the plugin version. Individual skill versions are given in the text.

### Plugin 1.3.2 (2026-10-30)

lead-qualifier-studi 1.1.2, after the second trial on the same law firm:

- **Namesakes without personal data.** Only profession and city, no full names or other details about people unrelated to the lead.
- **Existing relationship.** If the user already knows the lead, the output says so in one line after the summary and the next step becomes a direct contact. The verdict does not change.
- **Notes at the end.** Narrative text goes in an optional Notes section after the next step, never before the tables.
- **Decisive register.** If a ✅ register would change the verdict, the skill asks for the check before closing, or reports both verdicts.
- **Aggregators excluded.** Directories and sites that republish register data do not count as an institutional source.

### Plugin 1.3.1 (2026-10-30)

lead-qualifier-studi 1.1.1, after a trial on a real law firm:

- **Only three statuses.** No labels such as "❌ (partial)". Data not found, not even in search snippets, is ❌. Data found but unreadable (login wall, search form not responding) is ⚠️.
- **Register easier to verify.** If the local Ordine does not respond, the skill tries the national register of the profession and PDFs published on the Ordine's website. If the register stays ⚠️, the output gives the user the link to check it by hand; once confirmed, the register becomes ✅ and the verdict is recalculated.
- **Fixed values in the profile table.** No in-between values such as "Medium-high".
- **Summary line first.** The output opens with `Sintesi: [VERDICT]. [reason]`, then the tables. The full Verdict block stays.
- **Test cases.** New case for a LinkedIn profile that is found but cannot be read.

### Plugin 1.3.0 (2026-10-30)

lead-qualifier 1.3.0:

- **Main social instead of Twitter/X.** The first channel is the social network where the lead is most active, among X, Instagram, TikTok and LinkedIn. Before, a creator active only on Instagram, or a B2B founder active only on LinkedIn, got ❌ and risked a false REJECT.
- **YouTube gets a ⚠️ status.** A small channel (under 1,000 subscribers), or no channel in a business where video is not expected. The Section 6 table now covers both Trustpilot and YouTube, with a row for sellers of courses and info-products.
- **Decision table written in terms of the threshold.** The rows use the threshold S instead of the number 2, so changing the threshold no longer makes them contradictory. The threshold is set before the analysis.
- **Reputation search without a date filter.** The reputation query runs first without a year, then with the current year.

lead-qualifier-studi 1.1.0:

- **The register outweighs visibility.** With verified membership, LinkedIn ❌ and publications ❌ now give RISERVA instead of REJECT. REJECT still applies when the register cannot be verified either.
- **English trigger phrases**, as in lead-qualifier.
- **Verdict block aligned** with lead-qualifier.

Both:

- **Responsible use.** One line on informing the lead at first contact (GDPR, Art. 14).
- **Test cases.** New case for the B2B founder active only on LinkedIn; new case for the small firm with verified membership; lead-qualifier-studi case 2 rewritten for the new rule.

### Plugin 1.2.1 (2026-10-15)

- **English triggers.** The lead-qualifier description now includes English trigger phrases, so the skill also activates when the user writes in English. The instructions stay in Italian.

### Plugin 1.2.0 (2026-10-15)

- **New skill: lead-qualifier-studi 1.0.0.** A variant for members of professional bodies (Ordini) and professional firms. Channels: LinkedIn, professional register (Albo/Ordine), publications and events, with disambiguation of people with the same name.
- **Compared with the private version of lead-qualifier-studi:** ordered decision table (the first matching row wins), reputation affects the verdict, register ⚠️ separated from ❌ (register unavailable versus membership not found), litigation counted only when the firm itself is a party, fictional example, text independent of the author and of the search tool.
- **lead-qualifier 1.2.0.** Step 0 hands over to lead-qualifier-studi when the lead is a member of a professional body.
- **Test cases.** Eight cases for lead-qualifier-studi. For lead-qualifier, added the missing minor-signals case and the hand-over case.

### Plugin 1.1.0 (2026-10-15), first public release

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
