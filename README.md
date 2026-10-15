# claude-skills

[🇮🇹 Italiano](#italiano) · [🇬🇧 English](#english)

---

## Italiano

Skill per agenti AI, scritte da un Product Owner per problemi concreti di lavoro. Usano il formato aperto [Agent Skills](https://agentskills.io): funzionano in Claude e negli altri agenti compatibili. Le istruzioni delle skill sono in italiano.

### 📦 Skill disponibili

| Skill | Cosa fa | Versione |
|---|---|---|
| [lead-qualifier](plugins/lead-qualifier/skills/lead-qualifier/SKILL.md) | Decide se vale la pena contattare un lead: verifica tre canali pubblici e la reputazione, poi emette APPROVE, RISERVA o REJECT | 1.1.0 |

### 🎯 lead-qualifier

**Il problema.** Prima di scrivere a un potenziale cliente devi capire se è reale, attivo e affidabile. A mano servono 15-20 minuti e i criteri cambiano ogni volta. La skill fissa i criteri e li applica sempre allo stesso modo, con le fonti.

### 🧭 Come decide

Ogni canale (Twitter/X, YouTube, Trustpilot) riceve uno stato: ✅ positivo, ⚠️ non applicabile o incerto, ❌ assente o negativo. Poi vale la prima riga che corrisponde:

| Canali ❌ | Canali ⚠️ | Reputazione | Verdetto |
|---|---|---|---|
| 2 o più | qualsiasi | non si verifica | REJECT |
| 0 o 1 | qualsiasi | segnali critici | REJECT |
| 1 | qualsiasi | nessun segnale critico | RISERVA |
| 0 | 1 o più | nessun segnale critico | RISERVA |
| 0 | 0 | segnali minori | RISERVA |
| 0 | 0 | nessun segnale negativo | APPROVE |

**Cosa ottieni.** Una tabella canali, una scheda commerciale (credibilità, reputazione, budget probabile, rischio principale), il verdetto motivato e un next step di una riga. I [casi di test](examples/casi-di-test.md#italiano) mostrano un esempio per ogni verdetto.

### 🚀 Installazione

**Claude Code, come plugin**

```text
/plugin marketplace add Surfab/claude-skills
/plugin install lead-qualifier@surfab-skills
```

**Solo la skill.** Copia la cartella `plugins/lead-qualifier/skills/lead-qualifier/` nella cartella delle skill del tuo agente. In Claude Code è `~/.claude/skills/`. Nelle app Claude puoi caricarla come zip tra le skill personalizzate.

### 🔒 Limiti

- È calibrata su creator, founder e personal brand. Con PMI B2B e studi professionali lo segnala, e il verdetto diventa solo indicativo.
- Misura la presenza pubblica, non la solidità finanziaria.
- La qualità del verdetto dipende dalla ricerca web a disposizione dell'agente.

### 🛡 Uso responsabile

La skill lavora solo su informazioni pubbliche e pertinenti a una decisione commerciale, ed esclude dati personali estranei al business. Il verdetto dice se investire tempo in un contatto, non giudica la persona.

### 🗂 Struttura

```text
claude-skills/
├── .claude-plugin/
│   └── marketplace.json
├── plugins/
│   └── lead-qualifier/
│       ├── .claude-plugin/
│       │   └── plugin.json
│       └── skills/
│           └── lead-qualifier/
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

Agent skills written by a Product Owner for real work problems. They use the open [Agent Skills](https://agentskills.io) format, so they run in Claude and in other compatible agents. The skill instructions are written in Italian.

### 📦 Available skills

| Skill | What it does | Version |
|---|---|---|
| [lead-qualifier](plugins/lead-qualifier/skills/lead-qualifier/SKILL.md) | Decides whether a lead is worth contacting: checks three public channels and online reputation, then returns APPROVE, RISERVA or REJECT | 1.1.0 |

### 🎯 lead-qualifier

**The problem.** Before reaching out to a potential client you need to know whether they are real, active and reliable. By hand it takes 15-20 minutes, and the criteria change every time. The skill fixes the criteria and applies them the same way every time, with sources.

### 🧭 How it decides

Each channel (Twitter/X, YouTube, Trustpilot) gets a status: ✅ positive, ⚠️ not applicable or uncertain, ❌ missing or negative. The first matching row wins:

| ❌ channels | ⚠️ channels | Reputation | Verdict |
|---|---|---|---|
| 2 or more | any | not checked | REJECT |
| 0 or 1 | any | critical signals | REJECT |
| 1 | any | no critical signals | RISERVA |
| 0 | 1 or more | no critical signals | RISERVA |
| 0 | 0 | minor signals | RISERVA |
| 0 | 0 | no negative signals | APPROVE |

RISERVA is Italian for "with reservations": the lead is worth contacting, but only with a targeted approach.

**What you get.** A channel table, a commercial profile (credibility, reputation, likely budget, main risk), the verdict with its reasoning and a one-line next step. The [test cases](examples/casi-di-test.md#english) show one example for each verdict.

### 🚀 Installation

**Claude Code, as a plugin**

```text
/plugin marketplace add Surfab/claude-skills
/plugin install lead-qualifier@surfab-skills
```

**Skill only.** Copy the `plugins/lead-qualifier/skills/lead-qualifier/` folder into your agent's skills folder. In Claude Code that is `~/.claude/skills/`. In the Claude apps you can upload it as a zip among your custom skills.

### 🔒 Limits

- It is tuned for creators, founders and personal brands. With B2B SMEs and professional firms it flags the mismatch, and the verdict becomes indicative only.
- It measures public presence, not financial soundness.
- Verdict quality depends on the web search available to the agent.

### 🛡 Responsible use

The skill only works with public information relevant to a business decision, and leaves out personal data unrelated to the business. The verdict tells you whether a contact is worth your time. It does not judge the person.

### 🗂 Structure

```text
claude-skills/
├── .claude-plugin/
│   └── marketplace.json
├── plugins/
│   └── lead-qualifier/
│       ├── .claude-plugin/
│       │   └── plugin.json
│       └── skills/
│           └── lead-qualifier/
│               └── SKILL.md
├── examples/
│   └── casi-di-test.md
├── CHANGELOG.md
└── LICENSE
```

### 📝 License and author

[MIT](LICENSE). By Fabrizio Quaglio Cotti, Senior Product Owner, [github.com/Surfab](https://github.com/Surfab).
