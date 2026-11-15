# Netheret help desk, step 08: jobs

A teaching example. Over sixteen steps we build a help desk web app for
Netheret, a made-up company that supports the IT of small businesses. This
step lets a manager schedule on-site jobs for engineers and see a week of
jobs laid out like a calendar.

## What this step adds

- `helpdesk/jobs.py`, a new blueprint with:
  - `/jobs`: the week view, Monday to Sunday, with previous and next week
    links (`/jobs?week=2026-11-16` shows the week with that date in it);
  - `/jobs/new`: the form to schedule a job (managers only).
- `find_clash()`: an engineer cannot be booked for two jobs at once.
- `Job.scheduled_end` in `models.py`: the end time worked out from the start
  and the length, rather than stored twice.
- A "Schedule a job" button on a request's detail page, which fills in the
  company and request. The customer sees "An engineer will visit on..." on
  the request's timeline.

## Run it

```
python -m venv .venv
source .venv/bin/activate        # on Windows: .venv\Scripts\activate
pip install -r requirements.txt
python seed.py
flask --app helpdesk run --debug
```

Sign in as `manager@netheret.example` (demo password `password123`), open
Jobs, and schedule a job. Try booking the same engineer twice at the same
time to see the clash message.

## What to look at

- Two time ranges overlap when each one starts before the other one ends:
  `job.scheduled_start < end and start < job.scheduled_end`.
- `datetime.strptime` turns the text from a `datetime-local` box into a
  `datetime`, and a `ValueError` means it was not a real date and time.
- The chosen request must belong to the chosen company: the server checks
  that the pieces of the form agree with each other, not just each one alone.
- The week view uses CSS grid, so it is seven columns on a wide screen and
  one column on a phone, and each day is a section with a heading.

## Learn this step

This is step 8 of 16 of **Task 2. Developing the solution**, a free series of T Level Digital Software Development
lessons that builds the Netheret help desk in agile sprints with Python and Flask. Read the lesson for this step:
[Scheduling on-site jobs](https://mitsurutech.co.uk/resources/t-level/dsd-t2-08-jobs).

- Previous step: [step 07, assigning, escalating and the timeline](https://github.com/mitsurutech/netheret-helpdesk-07-timeline)
- Next step: [step 09, an engineer's schedule and job briefs](https://github.com/mitsurutech/netheret-helpdesk-09-my-schedule)
- [Every free T Level Digital lesson](https://mitsurutech.co.uk/resources/t-level)
- [Teach these lessons to your class on MitsuruTech](https://mitsurutech.co.uk/learning), [see the pricing](https://mitsurutech.co.uk/pricing) or
  [start a free year for your college](https://mitsurutech.co.uk/signup)

## About

Written by [Mitsuru Technologies](https://mitsurutech.co.uk) (MitsuruTech) as a teaching example for T Level Digital
Software Development. The Netheret IT Support Solutions brief is from Pearson's sample assessment material; this code
and its notes are our own, and are not published, endorsed or approved by Pearson or the Department for Education.
'T Level' is a registered trade mark of the Department for Education.

