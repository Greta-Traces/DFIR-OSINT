
---

# OSINT Methodology ~ Thinking Before You Click

**Date:** 2026-04-24 · **Category:** OSINT · **Level:** Beginner

---

## What was this about?

This writeup documents the investigative methodology I have been building as part of my OSINT learning path. It is not a tool guide. It is a framework for thinking or on how to approach an investigation before opening a single browser tab, how to move deliberately between data points, and how to know when to stop.

The methodology is structured around five core areas: mindset, the investigation process, pivot logic, pattern recognition, and documentation discipline. Each section reflects what I have learned from study, practice, and a fair amount of rabbitholes along the way.

---

## What did I know beforehand?

When I started OSINT felt out of reach. I did not know the difference between a domain and a DNS record and the investigative process looked like something that required years of professional experience before you could even begin. What kept me coming back was the puzzle aspect of it. The idea that information leaves traces and that those traces can be followed with the right approach. So I started taking it seriously and looking for a structured way to grow.

---

## What did I do?

My first instinct was to go straight to tools. Seemed easy, learn the tools and you can run an investigation. That turned out to be wrong. I ended up going in circles with no clear direction, searching without purpose, until I realised I needed to step back and build a proper foundation first.

It is easy to reach for Sherlock, GHunt, or Maltego. Tools feel like progress. But tools applied without a clear investigative question produce noise, not intelligence. A carelessly executed search can leave traces, alert a subject, or compromise findings before they are ever used. That is not hypothetical. It is why professional investigators think before they act.

The real discipline in OSINT is knowing **why** you are making each move and being able to reconstruct that reasoning later, especially if your findings need to hold up in a report or a legal context.

---

## What did I learn?

An investigation is a method not a toolbox. Not knowing how to document can make or break an entire process. I had to step back and learn how to approach an OSINT investigation before touching a single tool. In parallel I began working through structured OSINT training and things started to click.

An investigation follows a methodology, repeatable steps that keeps you on track and makes your process auditable.

### The investigation process at a glance

| Phase | Name               | Core activity                                                                           |
| ----- | ------------------ | --------------------------------------------------------------------------------------- |
| 0     | Preparation        | Define the research question. Inventory your seed data. Set scope. Run OPSEC checklist. |
| 1     | Passive collection | Gather from sources that leave no trace with the subject.                               |
| 2     | Structuring        | Stop searching. Build an entity map. Ask what you know versus what you assume.          |
| 3     | Pivoting           | Move deliberately from one data point to the next and document each step.               |
| 4     | Verification       | Confirm every finding with at least two independent sources.                            |
| 5     | Documentation      | Record everything, if you cannot reconstruct how you found it it has no value.          |

The most underestimated phase is Phase 0. A sharp research question is the difference between a productive session and hours of searching ending up with nothing.

### Pivot logic

A pivot is the movement from one data point to a new one. It sounds simple but in practice it requires discipline: 
- Every pivot should be intentional
- Traceable
- Tied to your original research question. 

Documenting each pivot in real time is what separates an investigation from a search session.

### Recognising patterns without tools

The most transferable skill I have developed is not tied to any specific tool. It is pattern recognition, noticing what is consistent, what is inconsistent and what is conspicuously absent.

Time patterns reveal timezone and routine. Language patterns like recurring phrasing, spelling habits, sudden style shifts can function as a fingerprint. Network patterns show which identities are genuinely connected versus which appear connected by coincidence.

The negative space matters just as much. An account that never reveals location while everyone around it does is making a choice. A profile that has existed for four years but contains only three weeks of activity is worth noting even if you cannot yet explain it.

I write these observations down immediately flagged clearly as a hypothesis not a finding. That distinction matters.

### Documentation discipline

I did not document anything in the beginning. I convinced myself I would figure it out later. Looking back I wish I had built the habit from day one. It can be difficult on a self-directed learning path with no one checking your work but everything gets documented now. Not because I expect every session to produce legally relevant material but because building the habit now means it will be automatic when it counts.

For each investigation I create a structured folder in Obsidian:

```
/cases/
└── case_[date]_[codename]/
    ├── 00_research_question.md
    ├── 01_timeline.md
    ├── 02_entities.md
    ├── 03_pivot_log.md
    ├── 04_sources.md
    ├── 05_unconfirmed.md
    ├── 06_summary.md
    └── screenshots/
```

Each data point gets its own entry: 
- Type
- Source
- Timestamp
- Screenshot
- Archive link
- Status
- What it leads to next 

If I cannot explain how I found something it does not go in the report. Chain of custody is not a concept reserved for courtroom professionals it is a habit built through consistent practice.

### Ethics and scope

OSINT gives access to a significant amount of information about real people. That access requires a clear defensible purpose and proportionate methods.

Before any investigation I ask four questions:

1. Is my purpose legitimate?
2. Am I using proportionate means?
3. Am I violating a reasonable expectation of privacy?
4. Could I explain my methods to a judge?

There is a hard line between passive research on publicly available information and active intrusion. The line is clear in principle and sometimes blurry in practice. When in doubt I do not cross it.

---

## Key takeaways

- **A research question is not optional.** Without a defined question every search produces data but no intelligence.
- **Document as you go not after.** If you cannot reconstruct the path the finding has no weight.
- **Pattern recognition is a skill not a tool.** It compounds with practice and applies across every platform and investigation type.

---

## Sources

- **Rae Baker** ~ _Deep Dive: Advanced Open Source Intelligence_ (book)  
	Structured my understanding of the investigation process and the importance of passive collection before active engagement
- **Brandon Brown** ~ OSINT-focused YouTube channel
	Ractical methodology walkthroughs and tool-in-context demonstrations
- **Dutch OSINT** ~ Blog posts and tutorials 
	Covering pivot techniques and investigative workflow in the OSINT community
- **Micah Hoffman** ~ Blog posts and tutorials
	Investigative methodology, documentation standards, and professional OSINT practice
- **Bellingcat** ~ bellingcat.com 
	Open source investigation in practice. Useful for seeing methodology applied to real cases

---

## Next steps

Platform-specific writeups, one per platform, same structure. Building toward a full OSINT reference library on GitHub.

---