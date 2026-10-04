# week-04/submission.yml — your declaration for this lab.
#
# Facts only. Every explanation goes in lab-report.md; nothing here repeats prose.
# Fill every value. Check it before you push:
#
#     python tests/validate_submission.py
#
# The validator checks shape, never quality. A green run is the floor, not the grade.
# If you cannot run Python, fill the file by hand against the comments — a malformed
# file costs you nothing if the content is there.

schema: 1
week: "04"

student:
  name:
  student_id:          # as in KBTU records, e.g. 24B031016
  github:              # your GitHub username, the one that owns the repo

assistant:
  tool:                # e.g. ChatGPT, Claude, Gemini, DeepSeek, Grok
  model:               # the exact model name with its version. "ChatGPT" is not a model name.

counts:
  behaviour_diagram:   # sequence | activity | both   (must match the files in models/)
  stories_source:      # week-03 | reference
  use_cases:           # how many use cases your REVISED use-case diagram has
  change_log_rows:     # rows in lab-report.md §8 (the task asks for 3 or more)

checker:
  # Numbers from YOUR last run of: python tests/check_models.py
  # They must add up to the number of checks it runs. Report them as they came out.
  # A FAIL you report and explain in lab-report.md costs you nothing. A hidden one costs the criterion.
  pass:
  fail:
  error:
  commit:              # the commit you ran the checker at: git rev-parse --short HEAD
                       # (normally the commit just before you commit this file — that is fine)
  kept_fails: []       # the check IDs that still FAIL and are explained in lab-report.md §9, e.g. [CL5]

assumptions:
  # The scenario does not settle these two. Decide, declare, and defend the decision in lab-report.md §4.3.
  # Either answer is acceptable. Not deciding is not.
  # (Week 03's third question, exactly two hours, is settled by R1 this week: "at most 2 hours" — allowed.)
  overlap_touching_bookings:   # allowed | not-allowed   (a booking ending 14:00 and one starting 14:00)
  blocking_a_booked_room:      # keep-bookings | cancel-bookings   (what R3 does to bookings that already exist)

traceability:
  # Empty lists are allowed — if you claim full coverage, the checker and I will test that claim.
  use_cases_not_traced: []     # use cases in your diagram with no approved story, e.g. [Login]
  rules_not_shown: []          # rules R1-R4 not visible in your behaviour diagram, e.g. [R3]

review_findings:
  # Three or more. One line each, and each one names the diagram element it is about.
  # Worthless: "the AI made mistakes in the class diagram".
  # Worth everything: "Room *-- Booking was a composition; a booking is not part of a room — plain association 1 / 0..*".
  -
  -
  -

honesty:
  originals_unedited:                 # yes | no   — models/original/ holds the AI's first replies as returned
  can_explain_everything_submitted:   # yes | no   — "no" is an accepted answer, name the part in lab-report.md
  ai_usage_disclosed:                 # yes | no   — AI_USAGE.md is required every week
