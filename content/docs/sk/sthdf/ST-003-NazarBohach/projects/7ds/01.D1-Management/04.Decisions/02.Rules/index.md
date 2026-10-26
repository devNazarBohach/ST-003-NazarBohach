---
# 🧩 Versioning – systém dopĺňa automaticky
fm_version: "1.0.1"

# Dátum buildu – generuje skript
fm_build: "2026-10-05T15:28:38.728453+00:00"

# Poznámka k verzii – voliteľné
fm_version_comment: ""


# 🆔 IDENTITY --------------------------------------------------------

# ID generuje CLI / skript

# Unikátne UUID – generuje skript
guid: "09eaba3b-7d91-40ae-8179-bd3fc44cb87c"


# 🧭 CONTEXT ---------------------------------------------------------

# DAO / doména (knife, sdlc, q12, 7ds...) dopĺňa skript
dao: "sthdf"

# Názov zápisu – dopĺňa používateľ
title: "02.Rules"

# Krátky popis – dopĺňa používateľ (voliteľné)
description: "Concrete HackLock team rules from KNIFE K000106: where each artifact lives (SSOT register), when a measurement counts (TSSOT), the shared glossary, change rules, and the SSOT check of 26 Oct 2026."


# 👥 AUTHORSHIP ------------------------------------------------------

# Hlavný autor – z globálneho configu
author: "Nazar Bohach"

# Zoznam autorov – generuje skript
authors:
  - "Nazar Bohach"


# 🗂 CLASSIFICATION ---------------------------------------------------

# Nadradená kategória – môže doplniť používateľ
category: ""

# Typ dokumentu (guide, case, tutorial...) – používateľ (voliteľné)
type: ""

# Priorita (low/medium/high) – voliteľné
priority: ""

# Tagy – odporúča sa 2–6 tagov.
# Typy tagov:
#   - rámce: knife, 7ds, sdlc, q12
#   - účel: tutorial, guide, pattern, case-study
#   - téma: git, backup, ai, communication
#   - úroveň: beginner, intermediate, advanced
tags: [7ds, knife, rules, ssot, hacklock]


# 🌍 LOCALIZATION -----------------------------------------------------

# Jazyk dokumentu – doplní skript podľa štruktúry
locale: "sk"


# 🕒 LIFECYCLE --------------------------------------------------------

# Dátum vytvorenia – generuje skript
created: "2026-10-05 18:28"

# Dátum poslednej úpravy – dopĺňa človek
modified: "2026-10-26 15:30"

# Stav dokumentu – default "backlog"
status: "in-progress"

# Viditeľnosť – default "public"
privacy: "public"


# ⚖ INTELLECTUAL PROPERTY -------------------------------------------

# Držiteľ práv k obsahu – dopĺňa skript
rights_holder_content: "Nazar Bohach"

# Systémový vlastník práv
rights_holder_system: "CAA / KNIFE / LetItGrow"

# Licencia
license: "CC-BY-NC-SA-4.0"

# Disclaimer
disclaimer: "Use at your own risk. Methods provided as-is; participation is voluntary and context-aware."

# Copyright
copyright: "© 2026 Nazar Bohach"


# 🔗 ORIGIN / PROVENANCE ---------------------------------------------

# Repozitár pôvodu
origin_repo: ""

# URL pôvodného repozitára
origin_repo_url: ""

# Commit pôvodu
origin_commit: ""

# Branch pôvodu
origin_branch: ""

# Systém pôvodu (CAA/KNIFE/STHDF…)
origin_system: "CAA"

# Pôvodný autor
origin_author: "Roman Kazicka"

# Importovaný zdroj
origin_imported_from: ""

# Dátum importu
origin_import_date: ""


# 🧱 RESERVED ---------------------------------------------------------

fm_reserved1: ""
fm_reserved2: ""
---

<!-- SDLC_INSTANCE_ID: ST-003-NazarBohach -->

# Rules

Concrete rules that put the [Principles](../01.Principles/index.md) into practice, mainly KNIFE [K000106 – SSOT and TSSOT](https://knifes.systemthinking.sk/en/knifes/K000106-SSOTandTSSOT/). Proposed on 26 Oct 2026; to be confirmed by the team.

Owners are given as **roles**. Who holds each role is written only in the Team section of the team README, so names are not repeated here.

## R1 – Where each thing lives (SSOT register)

The six SSOT questions (owner, master, how it is fed, how it is verified, who uses it, what happens on change), answered for each item:

| Item | Master: the only place it is edited | Owner | Verified by | Used by | On change |
|---|---|---|---|---|---|
| Scope and success criteria | team repo `docs/scope.md` | documentation & 7Ds | team review | Project Summary, presentations | edit there; other documents only link |
| Firmware: learning and hardened | team repo (today `tools/emulator/hacklock.ino`, later `firmware/`) | firmware & security | run in Wokwi, then on the board | Wokwi project, measurements | commit to the repo first, then copy into Wokwi |
| Wokwi project | not a master: a copy of the sketch from the repo | firmware & security | sketch in Wokwi matches the repo | demo, teammates without hardware | never edited only in Wokwi |
| Wiring, parts list, prices | team repo README → Hardware (later `hardware/`) | fabrication & enclosure | parts actually bought | scope, presentations | other documents link; prices are not repeated |
| Measurements: raw data, scripts, plots | team repo `measurements/` | firmware & security | the plot regenerates from the raw data (R2) | report, presentations | a new run gets a new dated folder; old runs stay |
| Team members, roles, PRJ number | team repo README → Team | documentation & 7Ds | confirmed by the teacher | Project Summary, About Me | edit there; other documents link |
| Glossary | this page, R3 | documentation & 7Ds | team review | code, README, docs, slides | change here first, then rename in code and docs |
| My deliverables (About Me, Knowledge Contribution, Reflexia) | this repository | me | – | course dashboard | – |

Team repository: [shot0071/brake-password](https://github.com/shot0071/brake-password)

## R2 – When a measurement counts (TSSOT)

A result is used in docs or presentations only if its dated folder in `measurements/` contains:

- raw data as CSV, one row per attempt;
- the commit of the script that collected the data and drew the plot;
- the firmware variant and its commit, with the values of `LEAK_US` and `RESP_US` used;
- the date, the setup (board or Wokwi) and the number of attempts;
- the plot, generated by the script from the raw data. No screenshots without data.

## R3 – Glossary: one term for one thing

| Use this term | Instead of | Meaning |
|---|---|---|
| HackLock | brake-password | the project and the team repository (rename pending) |
| learning firmware | weak, vulnerable, leaky, unsafe | build with `VULNERABLE 1`: early exit at the first wrong digit plus an artificial delay per correct digit |
| hardened firmware | fixed, safe, secure | build with `VULNERABLE 0`: constant-time comparison plus a fixed total response duration |
| attempt | try, guess | one PIN entry: digits ending with `#` on the keypad, or one serial line `TRY 1234` |
| response time | delay, timing | time measured **on the laptop** from sending a `TRY` line to receiving `OK` or `NO`; this is what the attack sees |
| check time | – | time measured **on the ESP32** with `micros()` around the PIN check; for debugging only, the attack never sees it |
| leak | – | the part of the response time that depends on how many leading digits were correct |
| `LEAK_US` | amplification | the artificial delay per correct digit in the learning firmware, in µs; its value lives only in the firmware |
| `RESP_US` | – | the fixed total response duration of the hardened firmware, in µs; its value lives only in the firmware |

## R4 – Change rules

- The real version of every file is the one in the repository. A file sent in a chat is only a draft.
- If a change makes another document wrong (a new pin, a new price, a renamed term), that document is fixed or flagged in the same commit.
- A firmware variant used for a measurement or a demo gets a git tag, for example `learning-v1` or `hardened-v1`, so results point to exact code.

## SSOT check – 26 Oct 2026

Comparison of the team repository with the rules above. Maturity on the K000106 scale (0–4): **level 2 – one source designated, other copies still exist**. Target for November: level 3 for firmware, parts list and team list; level 4 (trusted) for measurements.

| # | Finding | Fix | Owner |
|---|---|---|---|
| 1 | The budget appears three times with three values: README rows add up to about €12–19, the README total says about €25–30, the scope says about €15–20. | Agree on one figure; keep prices only in the README Hardware table; the scope links to it. | fabrication & enclosure |
| 2 | The README says an LED turns green on success; the sketch has only a red error LED. | Align the README with the sketch, or add a green LED to the design. | firmware & security |
| 3 | The README describes `python emulator.py` and `tools/emulator/README.md`, which do not exist; the folder holds only the Wokwi sketch. | Describe the Wokwi sketch as the current emulator, or add the script. | firmware & security |
| 4 | The README talks about a leak of a few microseconds but does not say that the learning firmware amplifies it to milliseconds with `LEAK_US`. | Explain the amplification and why it is needed over a serial link. | firmware & security |
| 5 | The same things have several names (see R3). | Use the glossary terms in code and docs. | everyone |
| 6 | The documentation & 7Ds role and the PRJ number are not filled in. | Assign the role; confirm the PRJ number and team with the teacher. | team |

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../../index.md)
