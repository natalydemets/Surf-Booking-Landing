# Surfing Booking Landing — QA Case Study

**Manual UI and API testing of a surf rental and booking web app, built by an agile team of six.**

**Natalie Demets** · Manual QA Engineer / TestRail Administrator · 2026

[![Surfing Booking QA showcase video](media/Surf_Booking_preview.gif)](media/Surf_Booking_QA_Portfolio_Revised.mp4)

▶️ **[Watch the 2-minute QA showcase video](media/Surf_Booking_QA_Portfolio_Revised.mp4)** · 🌐 **[Live demo](https://surf-booking-ten.vercel.app)**

## About the project

The app lets users check a surf forecast, choose rental packages for up to 10 surfers, add an instructor, book a session and complete a simulated payment. It also includes a live chat and a location map.

I covered the full QA lifecycle: requirements analysis, test design, TestRail administration, API testing in Postman, defect reporting in Jira, fix verification and the final regression before the team demo.

## Results at a glance

| Metric | Result |
| --- | --- |
| Test cases designed in TestRail | **359**: Home 166 · Booking 48 · Payment 27 · Chat 6 · REST API 112 |
| Automated API assertions in Postman | **421** |
| Requirements coverage | **14 user stories**, linked in a traceability matrix |
| Manual regression before the team demo | **150** key test cases |
| Final retest of selected Jira defects | **22** reviewed, **19** confirmed fixed |
| Defects documented | **52**, with steps, expected and actual results, and evidence |
| AI-assisted Playwright regression | **177** UI and API checks executed and analysed |
| Responsive coverage | 1440 px desktop · 768 px tablet · 375 px mobile |
| Browser engines | Chromium and WebKit |

> **Automation transparency:** the Playwright regression suite was created with AI assistance. My part was defining the scope and expected behaviour, running the suite, reviewing failures, comparing the results with manual and API testing, and documenting confirmed defects.

## Team and tech stack

| Area | Details |
| --- | --- |
| Project type | Educational team project |
| Team | QA Engineer, Frontend Developer, Backend Developer, Project Manager, Business Analyst, Designer |
| Process | Agile sprints; defect tracking and fix verification in Jira |
| Frontend | React + TypeScript ([repository](https://github.com/7uckingbad/Surf_booking)) |
| Backend | Java Spring Boot REST API + PostgreSQL ([repository](https://github.com/rmaksym1/surfing-booking-backend)) |
| Other | WebSocket/STOMP live chat, external weather API |
| QA tools | TestRail, Postman, Jira, Playwright, axe-core, Chrome DevTools |

This repository presents my QA work. The application code is maintained by the development team.

## What I did

- Analysed requirements and Figma designs, and clarified unclear behaviour with the team.
- Designed and maintained test cases for UI flows, business rules and API endpoints.
- Organised suites, sections and test runs as the TestRail administrator.
- Built a Postman collection for the Packs, Weather, Booking, Payment and Chat (Messages) APIs.
- Tested price calculations, field validation, package selection, participant limits and the simulated payment flow.
- Reported defects in Jira with reproduction steps, screenshots, logs and request/response evidence, linked to failed test cases.
- Retested fixes and ran regression across related features.
- Ran and analysed AI-assisted Playwright UI and API checks, and prepared the results for the team demo.

## From test case to verified fix

| Stage | Result |
| --- | --- |
| Test case | **C1186**: `POST /payment` should reject a cardholder name longer than 255 characters with HTTP 400 |
| Defects | **SBL-50 / SBL-51**: overlong payment fields returned HTTP 500. **SBL-49**: a missing `Idempotency-Key` header returned HTTP 500 |
| Evidence | Postman request and response, backend logs, expected and actual results in linked Jira reports |
| Fix | Backend [PR #7](https://github.com/rmaksym1/surfing-booking-backend/pull/7) added length validation and handling of a missing `Idempotency-Key` |
| Retest | The API now returns HTTP 400 with a clear validation message instead of HTTP 500 |

## Testing scope

| Feature | Focus |
| --- | --- |
| Home and navigation | Links, buttons, section navigation, layout and content |
| Forecast and calendar | Forecast display, date selection, month navigation, transfer of the selected date |
| Rental packages | Package details, prices, transfer to the booking form |
| Booking | Contact fields, participants, board selection, optional instructor, total price |
| Simulated payment | Required fields, validation, booking/payment integration, idempotency, error handling |
| REST API | Packs, Weather, Booking, Payment and Messages endpoints: CRUD, status codes, validation, pagination, persistence, error responses |
| Live chat | Joining with a name, message history, blank-message validation, timestamps, real-time delivery over WebSocket/STOMP |
| Location | Map loading and location details |
| Accessibility | Selected axe-core and keyboard checks |
| Responsive behaviour | Desktop, tablet and mobile viewports |

## Test design

**Techniques:** equivalence partitioning, boundary value analysis, positive and negative testing, decision-based business-rule testing, exploratory testing, API validation and persistence checks, cross-feature regression.

**Business rules covered, for example:**

- Board prices: Softboard **€40**, Hardboard **€55**, Performance **€70**.
- Optional instructor: **€20 per hour**.
- A booking takes up to **10 participants**; a request with 11 must be rejected.
- The total must reflect the selected boards and instructor hours.
- Repeated payment requests with the same idempotency key must not create duplicate payments.
- Invalid client input must return a controlled 4xx response, never HTTP 500.

## API testing in Postman

The collection covers the Packs, Weather, Booking, Payment and Chat (Messages) APIs, and its final run contained **421 automated assertions**. It includes:

- Positive CRUD scenarios and required-field validation.
- Invalid input and boundary values.
- Participant and price-calculation checks.
- Successful simulated payments, payment retrieval and pagination.
- Weather forecast requests: daily and range queries, date limits (today + 7 accepted, today + 8 rejected) and invalid date formats.
- Chat message history (`GET /messages`) with paging.
- Missing or malformed `Idempotency-Key` and duplicate-payment checks.
- Automatic test-data preparation, collection variables and chained requests.
- Assertions on status, response structure, values and persistence.

## Regression before the demo

1. **Manual regression:** 150 key TestRail cases, selected by risk and business importance.
2. **API regression:** the Postman collection run against the updated backend.
3. **Automated support:** 177 AI-assisted Playwright UI and API checks, run and analysed.
4. **Defect retest:** 22 selected Jira defects reviewed, 19 confirmed fixed.
5. **Cross-feature checks:** booking, payment, package selection, price calculation and API persistence verified together.

## Examples of defects found

Findings from testing; they do not necessarily reflect the current release.

| Area | Finding | Expected behaviour |
| --- | --- | --- |
| API validation | A booking with 11 participants returned HTTP 500 | Controlled client-validation response |
| API persistence | PATCH returned HTTP 200, but a following GET showed unchanged data | Persist and return the accepted update |
| Payment API | Overlong payment fields returned HTTP 500 (fixed in PR #7) | HTTP 400 with a clear message |
| Payment API | A missing `Idempotency-Key` returned HTTP 500 (fixed in PR #7) | Controlled client error |
| Booking UI | A Softboard package could produce a €0 total | Total calculated from the selected package |
| Booking UI | Package and instructor changes were not always reflected in the summary | Selections and total stay in sync |
| Forecast and booking | The selected date or package was not always carried over to the booking form | Keep the user's previous selection |
| Calendar | Past dates and invalid late times could be selected | Restrict selection to the booking rules |
| Performance | One home-page run transferred about 147.5 MB in 46 requests | Optimise images and resources for mobile |
| Chat | Message timestamps appeared in UTC | Show timestamps in the agreed time zone |
| Location | The interactive map did not load | Display the configured map |

## Repository contents

| Path | Contents |
| --- | --- |
| [`test-cases/`](test-cases/) | TestRail suite export (XML: 359 cases across Home, Booking, Payment, Chat and REST API, plus a 6-case trial Chat section) and the Home page cases (CSV) |
| [`media/`](media/) | QA showcase video and preview GIF |

Other materials from the project (the Postman collection, the traceability matrix, Jira reports and Playwright results) are not published here. Credentials, personal data and private Jira links are excluded.

## Links

- **Live application:** [surf-booking-ten.vercel.app](https://surf-booking-ten.vercel.app)
- **Frontend:** [7uckingbad/Surf_booking](https://github.com/7uckingbad/Surf_booking)
- **Backend:** [rmaksym1/surfing-booking-backend](https://github.com/rmaksym1/surfing-booking-backend)
- **Backend fix:** [PR #7](https://github.com/rmaksym1/surfing-booking-backend/pull/7)
- **QA portfolio:** [natalydemets/QA-Portfolio](https://github.com/natalydemets/QA-Portfolio)

## Contact

Open to Manual QA Engineer, backend and API testing roles, and freelance QA projects. More projects: [github.com/natalydemets](https://github.com/natalydemets).
