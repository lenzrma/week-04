# Week 04 — Lab report: Modeling the System with UML

> The single worksheet for this lab. Fill in every section. **Do not delete, rename or renumber
> the headings** — the checker and the grader find your work by them. Replace every `<...>`
> placeholder; a row that still contains `<...>` counts as empty.

---

## 1. Setup

| Field | Value |
| --- | --- |
| Name | <your name> |
| Group | <your group> |
| AI assistant | <e.g. Claude, ChatGPT, Gemini, DeepSeek, Grok> |
| Exact model | <the exact model name with its version, e.g. claude-sonnet-4-5> |
| Renderer | <PlantUML web server / VS Code extension / IntelliJ plugin / local jar> |
| Behaviour diagram | <sequence / activity / both> |
| Stories used | <my week-03 stories, revised / the reference set from README §3> |

---

## 2. Prompts as sent

Paste every prompt **exactly as you sent it**, in the order you sent it, one code block each. The
AI's first replies are saved as files in `models/original/` — do not paste them here.

### 2.1 Task 1 — use-case prompt

```text
<paste>
```

### 2.2 Task 2 — class prompt

```text
<paste>
```

### 2.3 Task 3 — behaviour prompt (3A sequence or 3B activity)

```text
<paste>
```

### 2.4 Focused correction prompts (if you sent any)

```text
<paste, or write "none">
```

### 2.5 Critique prompt

```text
<paste>
```

---

## 3. Task 1 — use-case review

**Assumptions the AI listed:** <one line each, or "the AI listed none" — that is a finding too>

At least **two** findings. A finding names the element, the problem and the rule or story that
proves it is a problem.

| # | Element | Problem | Rule or story | Fix |
| --- | --- | --- | --- | --- |
| 1 | <e.g. Student → Send confirmation> | <what is wrong> | <R4 / US-01 / scenario sentence> | <what you changed> |
| 2 | <element> | <problem> | <rule or story> | <fix> |

---

## 4. Task 2 — class diagram review

### 4.1 Relationships, read both ways

One row per association in your **revised** class diagram.

| Association | Read left → right | Read right → left | Multiplicities |
| --- | --- | --- | --- |
| <Student — Booking> | <one student makes 0..* bookings> | <each booking belongs to exactly 1 student> | <1 / 0..*> |
| <Room — Booking> | <...> | <...> | <...> |

### 4.2 Constraints the multiplicities cannot show

- R2: <how your diagram states it — which note, on which class>
- <any other rule that is not visible in multiplicities>

### 4.3 Assumptions

- A1: <an assumption you had to make — e.g. what happens to existing bookings when a room is blocked>
- <A2 ...>

### 4.4 Findings

| # | Element | Problem | Rule or story | Fix |
| --- | --- | --- | --- | --- |
| 1 | <element> | <problem> | <rule or story> | <fix> |

---

## 5. Task 3 — behaviour diagram review

**Option chosen and why:** <3A sequence / 3B activity — one sentence on why>

**Design components added beyond the domain model:** <name each one, e.g. `BookingService` —
what it does in one line; write "none" for an activity diagram>

| # | Element | Problem | Rule or story | Fix |
| --- | --- | --- | --- | --- |
| 1 | <element> | <problem> | <rule or story> | <fix> |

---

## 6. AI critique

Run the critique prompt once, on all your revised diagrams together. At least **three** rows. A
critique is another claim to evaluate, not a verdict: reject what is wrong and say why.

| # | Issue the AI raised | Element it cited | Verdict | Why |
| --- | --- | --- | --- | --- |
| 1 | <issue> | <element> | <accept / reject> | <your reason> |
| 2 | <issue> | <element> | <accept / reject> | <your reason> |
| 3 | <issue> | <element> | <accept / reject> | <your reason> |

---

## 7. Consistency table

One row for each of **R1–R4**, then one row for **every use case in your revised use-case
diagram**, spelled exactly as in the diagram, with the story ID it traces to.

| Requirement / story | Use case | Classes | Behaviour element |
| --- | --- | --- | --- |
| R1 | <use case> | <classes and attributes> | <message, guard or decision> |
| R2 | <use case> | <classes, note> | <message, guard or decision> |
| R3 | <use case> | <classes and attributes> | <message, guard or decision> |
| R4 | <use case> | <classes> | <message or action> |
| <US-01> | <Book room> | <Student, Booking, Room> | <message or action> |

---

## 8. Change log

At least **three** rows, and at least one for each required diagram (use case, class, your
behaviour diagram). "Before" is what the AI produced; "After" is what you submitted.

| # | Diagram | Before (AI's original) | After (your revision) | Reason |
| --- | --- | --- | --- | --- |
| 1 | <use case> | <before> | <after> | <rule, story or notation reason> |
| 2 | <class> | <before> | <after> | <reason> |
| 3 | <sequence / activity> | <before> | <after> | <reason> |

---

## 9. Checker output

Paste the complete output of `python tests/check_models.py`, then explain **every FAIL you are
keeping**. The same IDs go in `submission.yml` under `checker.kept_fails`. A FAIL you report and explain costs you nothing. One you hide costs the whole criterion.

```text
<paste the full output>
```

**FAILs I am keeping, and why:** <one line per check ID, or "none">

---

## 10. Conclusion (120–180 words)

<Which diagram did the AI get most wrong, and what exactly was wrong? Which error would have
reached the code if nobody had reviewed it? What did the critique find that you missed — and what
did it claim that was false? Be specific: "the AI got the multiplicities wrong" is worth nothing;
"the AI put 1..* on the Booking end, which says every room must already have a booking" is worth
everything.>
