---
# 🧩 Versioning – systém dopĺňa automaticky
fm_version: "1.0.1"

# Dátum buildu – generuje skript
fm_build: "2026-10-05T15:28:38.478701+00:00"

# Poznámka k verzii – voliteľné
fm_version_comment: ""


# 🆔 IDENTITY --------------------------------------------------------

# ID generuje CLI / skript

# Unikátne UUID – generuje skript
guid: "f85b0c54-bc9d-4ec5-a11a-b341d566e081"


# 🧭 CONTEXT ---------------------------------------------------------

# DAO / doména (knife, sdlc, q12, 7ds...) dopĺňa skript
dao: "sthdf"

# Názov zápisu – dopĺňa používateľ
title: "03.D3 Analysis"

# Krátky popis – dopĺňa používateľ (voliteľné)
description: "Context of the HackLock project (goal, people, process, technology, constraints) and good-enough technology choices, based on KNIFE K000103 (Context Aware Approach)."


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
tags: [7ds, knife, analysis, context, hacklock]


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

# D3 – Analysis

Context of the **HackLock** project, described *before* any technology decision, following KNIFE [K000103 – Context Aware Approach in SDLC](https://knifes.systemthinking.sk/en/knifes/K000103-CAA_IN_SDLC/).

Rule we follow: while the context is undefined, discussions about the "best" solution go nowhere. Once the context is written down, it gives us constraints and boundaries, and most decisions become quick.

Related pages: [Principles](../01.D1-Management/04.Decisions/01.Principles/index.md) · [Rules](../01.D1-Management/04.Decisions/02.Rules/index.md)

## 1. Context map

| Dimension | HackLock |
|---|---|
| **Goal** | A teaching aid: show a timing side-channel attack on *our own* keypad lock, measure it, then show the constant-time fix working. Not a real security product. |
| **People** | Three roles: firmware & security, fabrication & enclosure, documentation & 7Ds. Who holds each role is listed only in the team README (single source). Stakeholders: the course teacher, classmates as the demo audience, future students who rebuild the kit. |
| **Process** | STHDF course: 7Ds and SDLC documentation, visible weekly progress in Git, pitch and final presentation, deliverables by January. |
| **Technology** | ESP32, 4×4 keypad, SG90 servo, LED, buzzer; Arduino framework; Wokwi simulator; Python on the laptop for measurements; GitHub for all artifacts. |
| **Constraints** | Parts are paid from our own money (budget: see the Hardware table in the team README); enclosure made in the faculty FabLab; one semester; the demo must work live in a classroom. |
| **Ethics / scope** | Attacks only against our own firmware on our own board. |

Team repository: [shot0071/brake-password](https://github.com/shot0071/brake-password) (being renamed to HackLock).

## 2. What the context tells us

| Context fact | Consequence for the solution |
|---|---|
| Live classroom demo over a USB serial link | The natural timing difference is far below the noise of the serial link, so the learning firmware adds an artificial delay per correct digit (`LEAK_US`) to make the leak visible within seconds. |
| Own money, small budget | Cheap, common parts only; one servo opens a lid instead of a motorised bolt. |
| One semester, parts may arrive late | Simulator first (Wokwi), hardware second, so firmware and measurement tooling can start before the parts arrive. |
| Others must be able to rebuild it | Everything in one repository, documented step by step. |
| Teaching, not protection | No network, no app, no cloud: one serial link is enough. |

## 3. Good-enough technology choices

KNIFE K000103: no technology is perfect for every context. We compare options with the same criteria, in our context, and pick one that is good enough.

### Microcontroller board

| Criterion | ESP32 dev board | Arduino Nano |
|---|---|---|
| Fits the budget | yes | yes |
| Runs in Wokwi | yes | yes |
| Libraries for keypad and servo | yes (Keypad, ESP32Servo) | yes (Keypad, Servo) |
| Enough pins (keypad 8 + servo + LED + buzzer) | yes | yes |
| Timer resolution of `micros()` | 1 µs | 4 µs |
| Team know-how, existing code | sketch already written for ESP32 | none yet |
| Free toolchain (payment model) | yes | yes |

**Decision:** ESP32. It is already in our sketch and parts list, it runs in Wokwi and the team knows it. A Nano would also work; nothing in our context is a reason to switch.

### Tools by SDLC role

| Tool | Roles it serves | Why it fits our context |
|---|---|---|
| GitHub (team repo and personal repos) | everyone: code, docs, review, history | required by the course; one place for every artifact |
| Wokwi | firmware, testing | works before the parts arrive; free; shareable link |
| Arduino framework (ESP32 core) | firmware | keypad and servo libraries exist; the team knows it |
| Python | measurement, analysis | reads the serial port and plots results; the team knows it |
| FabLab (3D printer / laser cutter) | fabrication | available at the faculty |

## 4. Open questions

- PRJ number and the final team list: to be confirmed with the teacher.
- Who takes the documentation & 7Ds role.
- One agreed budget figure (see the SSOT check in [Rules](../01.D1-Management/04.Decisions/02.Rules/index.md)).

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../index.md)
