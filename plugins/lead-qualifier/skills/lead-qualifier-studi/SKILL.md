---
name: lead-qualifier-studi
description: Qualifica un lead che è un professionista iscritto a un Ordine o uno studio professionale (commercialisti, avvocati, notai, consulenti del lavoro) prima di un contatto commerciale. Verifica LinkedIn, iscrizione all'Albo e pubblicazioni o eventi, controlla la reputazione e restituisce un verdetto APPROVE, RISERVA o REJECT con fonti e un next step. Usala al posto di lead-qualifier per questi profili. Also use it when the user asks in English to qualify or vet an accountant, lawyer, notary or professional firm before sales outreach, for example "qualify this law firm" or "check this accountant before I contact them".
license: MIT
metadata:
  author: Fabrizio Quaglio Cotti
  version: "1.1.1"
---

# Lead Qualifier Studi Professionali

Variante di `lead-qualifier` per professionisti iscritti a un Ordine (commercialisti, avvocati, notai, consulenti del lavoro) e per gli studi associati.

La versione base misura social, YouTube e Trustpilot. Un professionista di studio quasi mai presidia quei canali, quindi applicata a questo segmento la regola scarta anche i lead buoni. Qui i tre canali obbligatori sono: **LinkedIn**, **Albo/Ordine**, **Pubblicazioni ed eventi**.

---

## 1. Obiettivo

Dato un professionista o uno studio, verifica identità, credibilità e potere decisionale prima di un contatto commerciale. Verdetto finale: **APPROVE**, **RISERVA** o **REJECT**.

### Stati dei canali

| Stato | Significato |
|---|---|
| ✅ | Positivo, verificato |
| ⚠️ | Parziale o incerto |
| ❌ | Assente o negativo |

Usa solo questi tre stati. Niente etichette aggiuntive come "❌ (parziale)" o "✅ con riserva": la nota sulla qualità del dato va nella colonna Dettaglio.

Distingui sempre tra dato **non trovato** e dato **non leggibile**:
- non trovato: nessun risultato, nemmeno negli snippet di ricerca → ❌
- non leggibile: il risultato esiste ma la pagina non si apre (login, modulo di ricerca che non risponde) → ⚠️

### Tabella di decisione

Applica la prima riga che corrisponde.

| Condizione | Verdetto |
|---|---|
| Albo ❌ (iscrizione non trovata sull'albo, oppure sanzione disciplinare pubblica) | **REJECT** immediato, a prescindere dagli altri canali |
| 2 canali ❌ e Albo ⚠️ | **REJECT** |
| Segnali critici da fonti terze (Step 3) | **REJECT** |
| 1 o 2 canali ❌ | **RISERVA** |
| 0 canali ❌ e 2 o più ⚠️ | **RISERVA** |
| 0 canali ❌, al massimo 1 ⚠️, segnali minori | **RISERVA** |
| 0 canali ❌, al massimo 1 ⚠️, nessun segnale negativo | **APPROVE** |

A differenza della versione base, qui un solo ⚠️ non blocca l'APPROVE: per uno studio è normale avere, per esempio, solo la pagina LinkedIn dello studio e non quella personale.

L'Albo pesa più della visibilità. Un professionista con iscrizione verificata ma senza LinkedIn e senza pubblicazioni è comune negli studi piccoli: è un lead reale, da contattare per email o telefono dello studio, quindi RISERVA e non REJECT. Il REJECT scatta solo se manca anche la verifica dell'iscrizione.

La tabella non si reinterpreta durante l'analisi.

---

## 2. Tono

- Diretto, senza preamboli.
- Dati prima, interpretazioni dopo. Ogni dato rilevante con la sua fonte.
- Riga di sintesi, poi tabelle e verdetto, prima di qualsiasi analisi narrativa.
- Italiano, professionale ma colloquiale.
- Niente aggettivi valutativi generici ("solido", "impressionante", "notevole"). Usa i dati.

---

## 3. Processo

### Step 0. Disambiguazione

Nomi comuni producono omonimi. Ancora l'identità a tre elementi: **studio, città, Ordine di iscrizione**.

- Se l'utente fornisce la pagina profilo sul sito dello studio, leggila per prima: è il punto di ancoraggio.
- Scarta ogni risultato che non combacia su almeno due dei tre elementi.
- Nell'output elenca in una riga gli omonimi scartati, così l'utente sa che non sono stati confusi col lead.

### Step 1. I tre canali obbligatori

Cerca sempre tutti e tre con lo strumento di ricerca web disponibile, anche se il lead sembra ovvio.

**LinkedIn**
- Query: `[nome] [studio] LinkedIn`, poi `[studio] LinkedIn`
- ✅ profilo personale con ruolo coerente e attività negli ultimi 12 mesi
- ⚠️ solo la pagina aziendale dello studio, oppure profilo personale fermo da oltre 12 mesi
- ⚠️ anche quando profilo o pagina compaiono nei risultati ma non si leggono senza login, e gli snippet non bastano a valutarli
- ❌ né profilo personale né pagina dello studio, nemmeno negli snippet di ricerca
- I profili LinkedIn spesso non si leggono senza login. Usa gli snippet di ricerca e scrivi nel Dettaglio che il dato è parziale.

**Albo / Ordine**
- Query: `[nome] Ordine [categoria] [città]`, poi la ricerca iscritti sul sito dell'Ordine territoriale
- Se il sito dell'Ordine territoriale non risponde, prova il registro nazionale della categoria: per gli avvocati l'albo del Consiglio Nazionale Forense, per i commercialisti l'albo unico del Consiglio Nazionale dei Dottori Commercialisti, per i notai la ricerca del Consiglio Nazionale del Notariato, per i consulenti del lavoro l'albo del loro Consiglio Nazionale
- Cerca anche `"[nome]" site:[dominio dell'Ordine]`: delibere, elenchi e verbali pubblicati in PDF spesso confermano l'iscrizione
- ✅ iscrizione verificata su fonte istituzionale. Cariche nel Consiglio o in commissioni dell'Ordine sono un segnale in più
- ⚠️ iscrizione dichiarata solo dal sito dello studio, con l'albo non consultabile né a livello territoriale né nazionale
- Quando l'Albo resta ⚠️, scrivi nell'output il link alla pagina di ricerca iscritti, così l'utente lo verifica a mano in un minuto. Se l'utente conferma l'iscrizione, l'Albo diventa ✅ e ricalcoli il verdetto
- ❌ iscrizione non trovata sull'albo, oppure sanzioni disciplinari pubbliche
- Il sito dello studio è fonte auto-dichiarata, l'Ordine è fonte terza. Tienile separate nell'output.

**Pubblicazioni ed eventi**
- Query: `[nome] relatore OR convegno`, `[nome] articolo [materia di competenza]`, sezioni Pubblicazioni ed Eventi del sito dello studio
- ✅ almeno un articolo, intervento a convegno o docenza verificabile degli ultimi 3 anni
- ⚠️ attività solo più vecchia di 3 anni, oppure data non verificabile
- ❌ nessuna traccia

X, YouTube e Trustpilot non sono criteri di squalifica per questo segmento. Se il professionista li usa, citalo come segnale in più.

### Step 2. Applica la regola

Conta ❌ e ⚠️. Se scatta una delle prime due righe della tabella di decisione, il verdetto è **REJECT**: salta Step 3 e 4 e vai all'output.

### Step 3. Reputazione

- Query: `[nome] [studio] sanzione disciplinare`, `[studio] recensioni`
- Query: `[studio] contenzioso OR indagine`, considerando solo i casi in cui lo studio o il professionista è parte in causa. Per un avvocato o un commercialista, le cause seguite per i clienti sono lavoro, non un segnale negativo.
- Recensioni dello studio su Google, se reperibili dalla ricerca.

Classifica il risultato:
- **Segnali critici**: frodi, truffe, mancati pagamenti o procedimenti che riguardano lo studio o il professionista, documentati da fonti terze attendibili
- **Segnali minori**: recensioni negative isolate, lamentele sporadiche
- **Nessun segnale negativo**: va scritto esplicitamente, è un dato

Poi applica la tabella di decisione.

### Step 4. Profilo commerciale

- **Ruolo nello studio**: socio fondatore, socio o collaboratore. Controlla in quale categoria compare sul sito (pagine "Soci" o "Professionisti"). Serve a capire chi decide il budget.
- **Studio**: anni di attività, sedi, numero di professionisti, certificazioni, network o partnership.
- **Nicchia**: aree di competenza concrete (es. revisione enti locali, crisi d'impresa, contenzioso tributario, M&A). È la base per l'angolo di contatto.
- **Segnali di rischio**: lead senza potere di spesa, studio piccolo con budget limitato, dati solo auto-dichiarati.

### Step 5. Output

Nell'ordine:
1. Riga di sintesi: `Sintesi: [VERDETTO]. [motivo principale in una frase]`
2. Tabella canali
3. Omonimi scartati (una riga)
4. Tabella profilo commerciale
5. Verdetto
6. Next step (una riga)

La riga di sintesi serve a chi legge di fretta. Non sostituisce il blocco Verdetto, che resta con il conteggio dei canali e la regola scattata.

---

## 4. Da fare e da evitare

**Da fare**
- Cerca sempre tutti e tre i canali.
- Distingui la fonte auto-dichiarata (sito dello studio) dalla fonte terza (Ordine, stampa, organizzatori di eventi).
- Indica sempre se il lead decide il budget o se serve arrivare a un socio.
- Lega il next step alla nicchia del professionista con un caso d'uso concreto sul suo lavoro (es. analisi documentale per la revisione, ricerca normativa, bozze di pareri). Niente pitch generico.
- Canale di contatto preferito: LinkedIn (personale o dello studio) o email professionale pubblicata dallo studio. Se LinkedIn è ❌, usa email o telefono dello studio.

**Da evitare**
- Non scambiare un omonimo per il lead.
- Non gonfiare i segnali positivi per compensare quelli mancanti.
- Non reinterpretare la tabella di decisione.
- Non proporre un contatto se il verdetto è REJECT.

---

## 5. Uso responsabile

- Usa solo informazioni pubbliche e professionali: ruolo, studio, iscrizione, competenze, pubblicazioni.
- Non riportare dati personali non professionali: data di nascita, indirizzo di casa, famiglia, salute, opinioni politiche o religiose.
- Il verdetto dice se investire tempo in un contatto. Non è un giudizio sulla persona.
- Nel primo contatto, chi usa la skill deve dire al lead da dove ha preso i suoi dati (GDPR, art. 14). La base giuridica tipica è il legittimo interesse.

---

## Template di output

### Sintesi

Sintesi: [APPROVE / RISERVA / REJECT]. [Motivo principale in una frase.]

### Tabella canali

| Canale | Stato | Dettaglio |
|---|---|---|
| LinkedIn | ✅ / ⚠️ / ❌ | Profilo personale o pagina studio, attività, fonte |
| Albo / Ordine | ✅ / ⚠️ / ❌ | Iscrizione, cariche, fonte istituzionale |
| Pubblicazioni ed eventi | ✅ / ⚠️ / ❌ | Titolo o evento, anno, fonte |

Omonimi scartati: [n, con descrizione di una parola ciascuno]

### Tabella profilo commerciale

Dove la tabella indica valori fissi (per esempio Alta / Media / Bassa), usa esattamente uno di quei valori, senza valori intermedi come "Media-alta". Le sfumature vanno nella motivazione.

| Aspetto | Segnale |
|---|---|
| Credibilità professionale | Alta / Media / Bassa |
| Iscrizione verificata da fonte terza | Sì / No |
| Ruolo e potere di spesa | Socio / Collaboratore / Non verificabile |
| Reputazione | Nessun segnale negativo / Segnali minori / Segnali critici |
| Nicchia | aree di competenza concrete |
| Budget probabile | stima di range dello studio |
| Rischio principale | descrizione sintetica |

### Verdetto

```text
VERDETTO: [APPROVE / RISERVA / REJECT]

Motivazione: [1-2 righe]

Canali ❌: [n su 3] · Canali ⚠️: [n su 3]
Regola scattata: [riga della tabella di decisione]
```

**Next step:** [Una riga. Canale, destinatario (il lead o un socio), angolo legato alla nicchia.]

---

## Esempio completo (lead fittizio, dati inventati)

Lead: commercialista in uno studio associato con trent'anni di attività.

Sintesi: RISERVA. Credenziali verificate dall'Ordine, ma potere di spesa non chiaro.

| Canale | Stato | Dettaglio |
|---|---|---|
| LinkedIn | ⚠️ | Solo la pagina dello studio (circa 1.000 follower). Profilo personale non trovato |
| Albo / Ordine | ✅ | Iscrizione e carica nel Consiglio verificate sul sito dell'Ordine territoriale |
| Pubblicazioni ed eventi | ⚠️ | Un intervento da relatore a un convegno, data non verificabile. Nessun articolo trovato |

Omonimi scartati: 3 (grafico, atleta, guida ambientale).

| Aspetto | Segnale |
|---|---|
| Credibilità professionale | Alta |
| Iscrizione verificata da fonte terza | Sì |
| Ruolo e potere di spesa | Non verificabile: dal sito non risulta se è socio |
| Reputazione | Nessun segnale negativo trovato |
| Nicchia | Revisione enti locali, fiscale, procedure concorsuali |
| Budget probabile | Medio-alto a livello di studio |
| Rischio principale | Potrebbe non decidere il budget |

```text
VERDETTO: RISERVA

Motivazione: nessun canale negativo, due parziali. Credenziali verificate da fonte terza, potere di spesa non chiaro.

Canali ❌: 0 su 3 · Canali ⚠️: 2 su 3
Regola scattata: 0 canali ❌ e 2 o più ⚠️ → RISERVA
```

**Next step:** verificare se è socio. Se no, contatto via LinkedIn verso un socio, con un caso d'uso sull'analisi documentale nella revisione degli enti locali.
