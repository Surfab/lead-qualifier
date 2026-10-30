# lead-qualifier

[🇮🇹 Italiano](#italiano) · [🇬🇧 English](#english)

---

## Italiano

Skill per agenti AI che qualificano un potenziale cliente prima del primo contatto commerciale. Decidono se vale la pena investirci tempo, con regole esplicite e fonti verificabili. Le ha scritte un Product Owner per un problema concreto di vendita.

Usano il formato aperto [Agent Skills](https://agentskills.io), quindi funzionano in Claude e negli altri agenti compatibili. Le istruzioni sono in italiano. Entrambe si attivano anche con richieste in inglese.

### 📦 Skill disponibili

| Skill | Per chi | Cosa verifica | Versione |
|---|---|---|---|
| [lead-qualifier](plugins/lead-qualifier/skills/lead-qualifier/SKILL.md) | Creator, founder, personal brand, aziende con pubblico consumer | Social principale (X, Instagram, TikTok o LinkedIn), YouTube, Trustpilot e reputazione | 1.3.0 |
| [lead-qualifier-studi](plugins/lead-qualifier/skills/lead-qualifier-studi/SKILL.md) | Professionisti iscritti a un Ordine e studi professionali | LinkedIn, Albo/Ordine, pubblicazioni ed eventi e reputazione | 1.1.0 |

Entrambe emettono APPROVE, RISERVA o REJECT, con le fonti e un next step.

### 🎯 Il problema

Prima di scrivere a un potenziale cliente devi capire se è reale, attivo e affidabile. A mano servono 15-20 minuti e i criteri cambiano ogni volta. Le skill fissano i criteri e li applicano sempre allo stesso modo, con le fonti.

I criteri giusti dipendono dal tipo di lead. Un commercialista quasi mai ha un canale YouTube, ma è iscritto a un Albo che si può verificare. Per questo le skill sono due.

### 🧭 Come decide

Ogni canale riceve uno stato: ✅ positivo, ⚠️ non applicabile o incerto, ❌ assente o negativo. Poi vale la prima riga che corrisponde. Le righe di lead-qualifier sono scritte con la soglia di default (2 canali ❌), che l'utente può cambiare prima dell'analisi.

**lead-qualifier**

| Canali ❌ | Canali ⚠️ | Reputazione | Verdetto |
|---|---|---|---|
| 2 o più | qualsiasi | non si verifica | REJECT |
| 0 o 1 | qualsiasi | segnali critici | REJECT |
| 1 | qualsiasi | nessun segnale critico | RISERVA |
| 0 | 1 o più | nessun segnale critico | RISERVA |
| 0 | 0 | segnali minori | RISERVA |
| 0 | 0 | nessun segnale negativo | APPROVE |

**lead-qualifier-studi**

| Condizione | Verdetto |
|---|---|
| Albo ❌ (iscrizione non trovata o sanzione disciplinare pubblica) | REJECT |
| 2 canali ❌ e Albo ⚠️ | REJECT |
| Segnali critici da fonti terze | REJECT |
| 1 o 2 canali ❌ | RISERVA |
| 0 canali ❌ e 2 o più ⚠️ | RISERVA |
| 0 canali ❌, al massimo 1 ⚠️, segnali minori | RISERVA |
| 0 canali ❌, al massimo 1 ⚠️, nessun segnale negativo | APPROVE |

Qui un solo ⚠️ non blocca l'APPROVE: per uno studio è normale avere solo la pagina LinkedIn dello studio e non quella personale. E l'Albo pesa più della visibilità: un piccolo studio con iscrizione verificata ma senza LinkedIn né pubblicazioni è RISERVA, non REJECT. Prima di tutto la skill separa il lead dagli omonimi, incrociando studio, città e Ordine.

**Cosa ottieni.** Una tabella canali, una scheda commerciale (credibilità, reputazione, budget probabile, rischio principale), il verdetto motivato e un next step di una riga. I [casi di test](examples/casi-di-test.md#italiano) mostrano un esempio per ogni riga delle due tabelle.

### 🚀 Installazione

**Claude Code, come plugin.** Il plugin installa entrambe le skill.

```text
/plugin marketplace add Surfab/lead-qualifier
/plugin install lead-qualifier@surfab-skills
```

**Solo le skill.** Copia una o entrambe le cartelle dentro `plugins/lead-qualifier/skills/` nella cartella delle skill del tuo agente. In Claude Code è `~/.claude/skills/`. Nelle app Claude puoi caricarle come zip tra le skill personalizzate.

### 🔒 Limiti

- lead-qualifier è calibrata su creator, founder e personal brand. Se il lead è un professionista iscritto a un Ordine rimanda a lead-qualifier-studi. Con le PMI B2B lo segnala, e il verdetto diventa solo indicativo.
- lead-qualifier-studi è pensata per gli Ordini professionali italiani.
- Le skill misurano la presenza pubblica, non la solidità finanziaria.
- La qualità del verdetto dipende dalla ricerca web a disposizione dell'agente.

### 🛡 Uso responsabile

Le skill lavorano solo su informazioni pubbliche e pertinenti a una decisione commerciale, ed escludono dati personali estranei al business. Al primo contatto va detto al lead da dove vengono i suoi dati (GDPR, art. 14). Il verdetto dice se investire tempo in un contatto, non giudica la persona.

### 🗂 Struttura

```text
lead-qualifier/
├── .claude-plugin/
│   └── marketplace.json
├── plugins/
│   └── lead-qualifier/
│       ├── .claude-plugin/
│       │   └── plugin.json
│       └── skills/
│           ├── lead-qualifier/
│           │   └── SKILL.md
│           └── lead-qualifier-studi/
│               └── SKILL.md
├── examples/
│   └── casi-di-test.md
├── CHANGELOG.md
└── LICENSE
```

### 📝 Licenza e autore

[MIT](LICENSE). Di Fabrizio Quaglio Cotti, Senior Product Owner, [github.com/Surfab](https://github.com/Surfab).

---

## English

Agent skills that qualify a potential client before the first sales contact. They decide whether a lead is worth your time, with explicit rules and verifiable sources. Written by a Product Owner for a real sales problem.

They use the open [Agent Skills](https://agentskills.io) format, so they run in Claude and in other compatible agents. The instructions are written in Italian. Both also trigger on requests written in English.

### 📦 Available skills

| Skill | For | What it checks | Version |
|---|---|---|---|
| [lead-qualifier](plugins/lead-qualifier/skills/lead-qualifier/SKILL.md) | Creators, founders, personal brands, consumer-facing companies | Main social (X, Instagram, TikTok or LinkedIn), YouTube, Trustpilot and reputation | 1.3.0 |
| [lead-qualifier-studi](plugins/lead-qualifier/skills/lead-qualifier-studi/SKILL.md) | Members of Italian professional bodies (Ordini) and professional firms | LinkedIn, professional register (Albo), publications and events, and reputation | 1.1.0 |

Both return APPROVE, RISERVA or REJECT, with sources and a next step.

### 🎯 The problem

Before reaching out to a potential client you need to know whether they are real, active and reliable. By hand it takes 15-20 minutes, and the criteria change every time. The skills fix the criteria and apply them the same way every time, with sources.

The right criteria depend on the type of lead. An accountant rarely has a YouTube channel, but they are listed in a professional register that can be checked. That is why there are two skills.

### 🧭 How it decides

Each channel gets a status: ✅ positive, ⚠️ not applicable or uncertain, ❌ missing or negative. The first matching row wins. The lead-qualifier rows assume the default threshold (2 ❌ channels), which the user can change before the analysis.

**lead-qualifier**

| ❌ channels | ⚠️ channels | Reputation | Verdict |
|---|---|---|---|
| 2 or more | any | not checked | REJECT |
| 0 or 1 | any | critical signals | REJECT |
| 1 | any | no critical signals | RISERVA |
| 0 | 1 or more | no critical signals | RISERVA |
| 0 | 0 | minor signals | RISERVA |
| 0 | 0 | no negative signals | APPROVE |

**lead-qualifier-studi**

| Condition | Verdict |
|---|---|
| Register ❌ (membership not found or public disciplinary sanction) | REJECT |
| 2 ❌ channels and register ⚠️ | REJECT |
| Critical third-party signals | REJECT |
| 1 or 2 ❌ channels | RISERVA |
| 0 ❌ channels and 2 or more ⚠️ | RISERVA |
| 0 ❌ channels, at most 1 ⚠️, minor signals | RISERVA |
| 0 ❌ channels, at most 1 ⚠️, no negative signals | APPROVE |

Here a single ⚠️ does not block APPROVE: it is normal for a firm to have only a company LinkedIn page and no personal profile. And the register outweighs visibility: a small firm with verified membership but no LinkedIn and no publications gets RISERVA, not REJECT. Before anything else, the skill separates the lead from people with the same name by matching firm, city and professional body.

RISERVA is Italian for "with reservations": the lead is worth contacting, but only with a targeted approach.

**What you get.** A channel table, a commercial profile (credibility, reputation, likely budget, main risk), the verdict with its reasoning and a one-line next step. The [test cases](examples/casi-di-test.md#english) show one example for each row of both tables.

### 🚀 Installation

**Claude Code, as a plugin.** The plugin installs both skills.

```text
/plugin marketplace add Surfab/lead-qualifier
/plugin install lead-qualifier@surfab-skills
```

**Skills only.** Copy one or both folders inside `plugins/lead-qualifier/skills/` into your agent's skills folder. In Claude Code that is `~/.claude/skills/`. In the Claude apps you can upload them as zips among your custom skills.

### 🔒 Limits

- lead-qualifier is tuned for creators, founders and personal brands. When the lead is a member of a professional body it hands over to lead-qualifier-studi. With B2B SMEs it flags the mismatch, and the verdict becomes indicative only.
- lead-qualifier-studi is designed for Italian professional bodies.
- The skills measure public presence, not financial soundness.
- Verdict quality depends on the web search available to the agent.

### 🛡 Responsible use

The skills only work with public information relevant to a business decision, and leave out personal data unrelated to the business. At first contact, tell the lead where their data came from (GDPR, Art. 14). The verdict tells you whether a contact is worth your time. It does not judge the person.

### 🗂 Structure

```text
lead-qualifier/
├── .claude-plugin/
│   └── marketplace.json
├── plugins/
│   └── lead-qualifier/
│       ├── .claude-plugin/
│       │   └── plugin.json
│       └── skills/
│           ├── lead-qualifier/
│           │   └── SKILL.md
│           └── lead-qualifier-studi/
│               └── SKILL.md
├── examples/
│   └── casi-di-test.md
├── CHANGELOG.md
└── LICENSE
```

### 📝 License and author

[MIT](LICENSE). By Fabrizio Quaglio Cotti, Senior Product Owner, [github.com/Surfab](https://github.com/Surfab).
