# Week 04 — Lab report: Modeling the System with UML

> The single worksheet for this lab. Fill in every section. **Do not delete, rename or renumber
> the headings** — the checker and the grader find your work by them. Replace every `<...>`
> placeholder; a row that still contains `<...>` counts as empty.

---

## 1. Setup

| Field | Value |
| --- | --- |
| Name | Kuralay |
| Group | Monday from 16:00-19:00 |
| AI assistant | Gemini |
| Exact model | Gemini Flash-Lite |
| Renderer | PlantUML web server |
| Behaviour diagram | sequence |
| Stories used | the reference set from README §3 |

---

## 2. Prompts as sent

Paste every prompt **exactly as you sent it**, in the order you sent it, one code block each. The
AI's first replies are saved as files in `models/original/` — do not paste them here.

### 2.1 Task 1 — use-case prompt

Using the supplied scenario and approved stories, generate PlantUML for a use-case diagram. Include Student and Administrator outside a named system boundary. Model their goals, show justified associations, and list assumptions. Use include or extend only with a clear reason.

### 2.2 Task 2 — class prompt

Create a UML domain class diagram in PlantUML for Smart Campus. Start with Student, Room, and Booking. Add attributes, appropriate operations, and association multiplicities. Add other classes only when requirements justify them. Explain each relationship and list assumptions. Avoid unjustified inheritance or composition.

### 2.3 Task 3 — behaviour prompt (3A sequence or 3B activity)

Generate PlantUML for Book room. Use Student, BookingService, and BookingRepository lifelines. Validate the supplied rules, then attempt the reservation. Show a successful confirmation and an unavailable-room alternative using alt. Label messages and replies. Explain new design components and all assumptions.

### 2.4 Focused correction prompts (if you sent any)

NONE!

### 2.5 Critique prompt

Review the use-case, class, and sequence models for Smart Campus against the scenarios, rules R1-R4, and UML best practices. List structural or logical flaws, missing relationships, or rule violations, and provide concrete recommendations for improvement.



## 3. Task 1 — use-case review

**Assumptions the AI listed:** 
- The system scope is strictly limited to room booking, cancellation, and administrative blocking, excluding external payment gateways.
- Rules R1-R3 are enforced within booking logic rather than standalone pre-checks.

At least **two** findings. A finding names the element, the problem and the rule or story that
proves it is a problem.

| # | Element | Problem | Rule or story | Fix |
| --- | --- | --- | --- | --- |
| 1 | Student -> Produce confirmation | AI connected the actor directly to the confirmation use case, but users only trigger booking. | R4 | Removed direct association and used an <<include>> link from Book room to Produce confirmation. |
| 2 | Administrator -> Block Room / Unblock Room | The AI split blocking and unblocking into two separate use cases, cluttering the diagram. | US-04, US-05 | Combined them into a single coherent "Block / unblock room" use case. |




## 4. Task 2 — class diagram review

### 4.1 Relationships, read both ways

One row per association in your **revised** class diagram.

| Association | Read left → right | Read right → left | Multiplicities |
| --- | --- | --- | --- |
| Student — Booking | One student makes zero or more bookings | Each booking belongs to exactly one student | 1 to 0..* |
| Room — Booking | One room has zero or more bookings | Each booking is associated with exactly one room | 1 to 0..* |
| Administrator — Room | One administrator manages zero or more rooms | Each room is managed by one administrator | 1 to * |

### 4.2 Constraints the multiplicities cannot show

- R2: Active bookings for the same room cannot overlap, stated via a note attached to the Booking class.
- R1: Time duration must be greater than 0 and less than or equal to 2 hours with a future start time, handled via method logic.
- R3: A blocked room cannot accept a new booking, enforced via the `isBlocked` attribute check.

### 4.3 Assumptions

- A1: A room can exist without any active bookings (0..* multiplicity).
- A2: Deleting a student record cascades or retains history according to system retention policy.

### 4.4 Findings

| # | Element | Problem | Rule or story | Fix |
| --- | --- | --- | --- | --- |
| 1 | Room attributes | Initial AI model lacked the `isBlocked` flag required to enforce rule R3. | R3 | Added `isBlocked: boolean` attribute and `setBlocked()` method to the Room class. |
| 2 | Booking attributes | Initial model missed explicit tracking fields for booking state and times. | R1, R2 | Added `startTime`, `endTime`, and `status` attributes to the Booking class. |






## 5. Task 3 — behaviour diagram review

**Option chosen and why:** 3A sequence — chosen because it clearly illustrates message exchanges and lifeline interactions for validating rules R1-R3 and the alternative failure paths.

**Design components added beyond the domain model:** 
- `BookingService`: Coordinates the booking workflow, validates business rules (R1-R3), and handles repository interactions.
- `BookingRepository`: Manages data persistence operations for checking availability and saving bookings.

| # | Element | Problem | Rule or story | Fix |
| --- | --- | --- | --- | --- |
| 1 | Alternative block (alt) | Initial AI model included an unsafe branch where booking failure still triggered a save operation. | R2, R3, SQ4 | Corrected the `alt` block so that the failure branch (`else`) directly returns an error without calling `saveBooking`. |
| 2 | Guard conditions | Missing explicit guard expression on the failure path of the `alt` block. | R1-R3 | Added clear condition descriptions to the failure branch. |




## 6. AI critique

Run the critique prompt once, on all your revised diagrams together. At least **three** rows. A
critique is another claim to evaluate, not a verdict: reject what is wrong and say why.

| # | Issue the AI raised | Element it cited | Verdict | Why |
| --- | --- | --- | --- | --- |
| 1 | Suggests adding an explicit Payment system actor and use-case | Payment / Billing | Reject | Out of scope according to the project requirements and boundaries. |
| 2 | Suggests adding method parameters and return types to all class operations | Class operations | Accept | Improves clarity and implementation details in the domain model. |
| 3 | Suggests splitting the sequence diagram into multiple separate diagrams for success and failure | Sequence lifeline | Reject | A single sequence diagram with an `alt` block is more concise and clearly shows both paths together. |




## 7. Consistency table

One row for each of **R1–R4**, then one row for **every use case in your revised use-case
diagram**, spelled exactly as in the diagram, with the story ID it traces to.

| Requirement / story | Use case | Classes | Behaviour element |
| --- | --- | --- | --- |
| R1 | Book room | Booking (`startTime`, `endTime`) | Validation rule in service |
| R2 | Book room | Booking, Room (note) | Overlap check in sequence |
| R3 | Book room / Block / unblock room | Room (`isBlocked`) | Block check before save |
| R4 | Book room | Booking, Confirmation | `bookingConfirmation` message |
| US-01 | View room availability | Student, Room | `viewAvailability()` method |
| US-02 | Book room | Student, Room, Booking | `requestBooking()` message |
| US-03 | Cancel booking | Student, Booking | `cancelBooking()` method |
| US-04 | Block / unblock room | Administrator, Room | `setBlocked()` method |
| US-05 | Block / unblock room | Administrator, Room | `blockRoom()` / `unblockRoom()` |
| US-06 | Review usage | Administrator, Room | `reviewUsage()` method |



## 8. Change log
At least **three** rows, and at least one for each required diagram (use case, class, your
behaviour diagram). "Before" is what the AI produced; "After" is what you submitted.
| # | Diagram | Before (AI's original) | After (your revision) | Reason |
| --- | --- | --- | --- | --- |
| 1 | Use-case | Actors placed inside system boundary and confirmation connected directly to student | Actors placed outside boundary; confirmation linked via <<include>> from booking | UML standard compliance and rule R4 adherence |
| 2 | Class | Missing `isBlocked` attribute in Room and tracking attributes in Booking | Added `isBlocked: boolean` and core fields (`startTime`, `endTime`, `status`) | Required to enforce rules R1, R2, and R3 |
| 3 | Sequence | Failure branch (`else`) incorrectly executed `saveBooking` | Failure branch returns `reject` directly without saving | Correcting logic flow so failed reservations are not persisted (SQ4) |



## 9. Checker output
Paste the complete output of `python tests/check_models.py`, then explain **every FAIL you are
keeping**. The same IDs go in `submission.yml` under `checker.kept_fails`. A FAIL you report and explain costs you nothing. One you hide costs the whole criterion.
NONE!



## 10. Conclusion
The AI struggled most with the sequence diagram, where it generated a critical flaw inside the conditional `alt` block: the failure branch (`else`) incorrectly attempted to execute the `saveBooking` operation before returning a rejection message. If left unreviewed, this severe logic bug would have directly reached the code implementation phase, causing the system to persist invalid, conflicting, or overlapping reservations into the database while completely bypassing strict business rules R2 and R3. 
During the multi-model critique phase, the analysis successfully uncovered that the initial domain class diagram lacked essential tracking attributes, such as `startTime`, `endTime`, and `status` inside the Booking class, which we initially overlooked. However, the AI's automated critique also raised a false claim by suggesting the inclusion of a separate external Payment system actor and billing use-case, which was correctly rejected as entirely out of scope. Ultimately, rigorous human architectural review proved absolutely essential to bridge the critical gap between high-level generative AI output and strict system design consistency.