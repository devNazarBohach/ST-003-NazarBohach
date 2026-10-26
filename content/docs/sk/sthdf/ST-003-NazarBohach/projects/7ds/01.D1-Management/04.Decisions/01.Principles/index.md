---
# 🧩 Versioning – systém dopĺňa automaticky
fm_version: "1.0.1"

# Dátum buildu – generuje skript
fm_build: "2026-10-05T15:28:38.720322+00:00"

# Poznámka k verzii – voliteľné
fm_version_comment: ""


# 🆔 IDENTITY --------------------------------------------------------

# ID generuje CLI / skript

# Unikátne UUID – generuje skript
guid: "7721b07f-7d80-411a-a2d8-ca76a589cd0c"


# 🧭 CONTEXT ---------------------------------------------------------

# DAO / doména (knife, sdlc, q12, 7ds...) dopĺňa skript
dao: "sthdf"

# Názov zápisu – dopĺňa používateľ
title: "01.Principles"

# Krátky popis – dopĺňa používateľ (voliteľné)
description: "How the HackLock team works: principles taken from KNIFE K000103 (Context Aware Approach, V-Model), K000101 (Cynefin) and K000106 (SSOT and TSSOT), applied to our project."


# 👥 AUTHORSHIP ------------------------------------------------------

# Hlavný autor – z globálneho configu
author: "Nazar Bohach"

# Zoznam autorov – generuje skript
authors:
  - "Nazar Bohach"
  - "Mykola Malesh"
  - "Viktor Hutsuliak"


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
tags: [7ds, knife, principles, caa, ssot, hacklock]


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

# Principles

How the HackLock team works. Each principle comes from a KNIFE article and is written here the way it applies to our project. The concrete rules that follow from them are in [Rules](../02.Rules/index.md); the project context is in [D3 – Analysis](../../../03.D3-Analysis/index.md).

Sources: [K000103 – Context Aware Approach in SDLC](https://knifes.systemthinking.sk/en/knifes/K000103-CAA_IN_SDLC/) · [K000106 – SSOT and TSSOT](https://knifes.systemthinking.sk/en/knifes/K000106-SSOTandTSSOT/) · [K000101 – Cynefin](https://knifes.systemthinking.sk/en/knifes/K000101-CYNEFIN_Framework/)

## P1 – Communication comes first

The CAA chain: communication → understanding → trust → collaboration → synergy → success. A missing link early on breaks everything after it.

**For us:** decisions are not only said in a call or a chat; they are written down (in this 7Ds section or as a GitHub issue), so a teammate who was not there can follow them.

## P2 – Context before technology

Every solution lives in a context: people, process, technology, constraints. We describe it first ([D3 – Analysis](../../../03.D3-Analysis/index.md)) and choose what is *good enough for this context*, not what is "best" in general.

**For us:** every technology choice in our docs names the context facts it relies on (budget, live demo, one semester, rebuildable by others).

## P3 – Every phase of the V, each with its check

Every solution passes through the V-Model phases, from idea to change management. How deep each phase goes depends on the project, but no phase is skipped without saying so. Each phase on the left side of the V has a matching check on the right side.

| Phase (left side of the V) | HackLock artifact | Checked by (right side of the V) |
|---|---|---|
| Idea / goal | Scope and success criteria (team repo `docs/scope.md`) | Acceptance: the success criteria shown live at the final presentation |
| High-level design | System picture: keypad → ESP32 → servo and LED; laptop ↔ ESP32 over serial | System test: full attack and full fix on real hardware |
| Analysis | Requirements: the leak is measurable on the learning firmware and not measurable on the hardened firmware | Measurement report with raw data ([Rules](../02.Rules/index.md), R2) |
| Detailed design | PIN check variants, serial `TRY` protocol, wiring | Integration test: both variants run in Wokwi, then on the board |
| Implementation | Firmware, measurement script, enclosure | Checks of the PIN function with correct, wrong and partially correct PINs |
| Operations | Classroom demo, rebuild guide | A person outside the team rebuilds the kit from the repository |
| Change management | Git history, tags for firmware variants | Change log and Reflexia |

## P4 – One picture is worth a thousand words

There is no good solution without pictures. Each important part gets one: the system diagram, the wiring diagram, and above all the **response-time plot**, which shows the leak in the learning firmware and its absence in the hardened firmware side by side. That plot is the main picture of the whole project.

## P5 – Probe → Sense → Respond for what we cannot plan

Most of our work is ordered: wiring, flashing, coding a known fix. One part is complex (Cynefin): how the timing difference behaves in the noise of the USB serial link, and how small it can get before it disappears. We do not plan that part in detail up front; we run short cycles:

1. **Probe:** measure many attempts with a correct first digit and with a wrong first digit.
2. **Sense:** compare the two distributions. Is the difference clearly above the noise?
3. **Respond:** change one thing (number of attempts, `LEAK_US`, where the time is taken) and repeat.

Each cycle is one short, dated entry with its raw data in the team repo `measurements/`.

## P6 – One source of truth for each thing (SSOT)

For every piece of information there is exactly one place where it is edited. Everywhere else *links* to it instead of copying it. SSOT is a team decision first and a tooling question last.

**For us:** project artifacts (code, wiring, parts and prices, measurements, team list) live in the team repository. My 7Ds pages and deliverables link to them and do not copy code, numbers or names. The full register is in [Rules](../02.Rules/index.md), R1.

## P7 – A source we can trust (TSSOT)

A single source is not enough if nobody can check it. A measurement result counts only if anyone can regenerate it: raw data, the script, the firmware version and the date are stored together.

**For us:** no screenshots of plots without data. Details in [Rules](../02.Rules/index.md), R2.

## P8 – One shared vocabulary

When the same thing has several names, or one name means different things, people stop understanding each other.

**For us:** one term for one thing, the same in code, README, docs and slides. Our glossary is in [Rules](../02.Rules/index.md), R3.

## P9 – AI amplifies what it gets

AI does not check its input; it produces confident output from whatever it is given. With inconsistent sources it produces wrong answers faster.

**For us:** we use AI for drafts of text and code, but only on top of our repository (the SSOT), and a person checks every result. Measurement conclusions and the reflection are written and understood by us.

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../../index.md)
