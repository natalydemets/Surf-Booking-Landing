# Surfing Booking Landing — QA Case Study

**Manual UI and API testing for an educational team web application.**

**Author:** Natalie Demets  
**Role:** Manual QA Engineer / TestRail Administrator  
**Year:** 2026

[![Surfing Booking QA showcase video](media/Surf_Booking_preview.gif)](media/Surf_Booking_QA_Portfolio_Revised.mp4)

▶️ **[Watch the 2-minute QA showcase video](media/Surf_Booking_QA_Portfolio_Revised.mp4)** — a walkthrough of the application, test design, API testing process, defects, and final results.

🌐 **Live demo:** [surf-booking-ten.vercel.app](https://surf-booking-ten.vercel.app)

I tested the Surfing Booking Landing web application throughout the full QA lifecycle—from requirements analysis and test design to defect reporting, fix verification, and final regression testing.

My contribution included 359 TestRail test cases, a Postman collection with 421 automated API assertions, 150 key manual regression cases, and the execution and analysis of an AI-assisted Playwright regression suite containing 177 UI and API checks.

The application allows users to explore a surf forecast, choose rental packages for up to 10 surfers, add an instructor, create a booking, and complete a simulated payment. It also includes live chat, location information, and an interactive map.

## Results at a glance

| Metric | Result |
| --- | --- |
| Test cases designed in TestRail | **359 total:** Home 166 · Booking 48 · Payment 27 · Chat 6 · REST API 112 |
| Automated API assertions in Postman | **421** |
| Requirements coverage | **14 user stories** covered and linked in a traceability matrix |
| Manual regression before the team demo | **150 key test cases** |
| Final retest of selected Jira defects | **22 reviewed; 19 confirmed fixed** |
| Defects documented during the project | **52**, with reproduction steps, expected and actual results, and evidence |
| AI-assisted Playwright regression | **177 UI and API checks executed and analysed** |
| Responsive coverage | **1440 px desktop · 768 px tablet · 375 px mobile** |
| Browser engines | **Chromium and WebKit** |

> **Automation transparency:** The Playwright regression suite was created with AI assistance. My contribution included defining the testing scope and expected behaviour, executing the suite, reviewing failures, comparing automated results with manual and API testing, and documenting confirmed defects.

## Project overview

| Area | Details |
| --- | --- |
| Project type | Educational team project |
| Team | QA Engineer, Frontend Developer, Backend Developer, Project Manager, Business Analyst, Designer |
| Process | Agile sprints; defect tracking and fix verification in Jira |
| Frontend | React and TypeScript ([repository](https://github.com/7uckingbad/Surf_booking)) |
| Backend | Java Spring Boot REST API and PostgreSQL ([repository](https://github.com/rmaksym1/surfing-booking-backend)) |
| Other components | WebSocket/STOMP live chat and external weather API integration |
| Testing tools | TestRail, Postman, Jira, Playwright, axe-core, Chrome DevTools |
| Test design techniques | Equivalence partitioning, boundary value analysis, positive and negative testing, exploratory testing |

This repository presents my QA contribution. The application source code is maintained by the development team.

## My responsibilities

- Analyse requirements and Figma designs, identify unclear behaviour, and discuss questions with the team.
- Design and maintain test cases and checklists for UI flows, business rules, and API endpoints.
- Organise test documentation, sections, suites, and test runs as the TestRail administrator.
- Create and maintain a Postman collection for Packs, Booking, and Payment API endpoints.
- Test booking calculations, field validation, package selection, participant limits, and simulated payment flows.
- Verify REST API responses, HTTP status codes, validation rules, idempotency, pagination, and data persistence.
- Report defects in Jira with clear reproduction steps, expected and actual results, screenshots, logs, and request/response evidence.
- Link failed test cases with Jira defects and maintain requirement traceability.
- Retest backend and frontend fixes and perform regression testing across related functionality.
- Execute and analyse AI-assisted Playwright UI and API regression checks.
- Prepare testing results and evidence for the final team demonstration.

## From test case to verified fix

One example of how my QA work contributed to improving the product:

| Stage | Result |
| --- | --- |
| Test case | **C1186:** `POST /payment` should reject a cardholder name longer than 255 characters with HTTP 400 |
| Defects | **SBL-50 / SBL-51:** overlong payment fields returned HTTP 500; **SBL-49:** a missing `Idempotency-Key` header returned HTTP 500 |
| Evidence | Postman request and response, backend logs, expected/actual results, and linked Jira reports |
| Fix | Backend [PR #7](https://github.com/rmaksym1/surfing-booking-backend/pull/7) added maximum-length validation and controlled handling of a missing `Idempotency-Key` |
| Retest result | The API returned HTTP 400 with a controlled validation response instead of HTTP 500 |

## Testing scope

| Feature | Testing focus |
| --- | --- |
| Home and navigation | Links, buttons, section navigation, responsive layout, and content |
| Forecast and calendar | Forecast display, date selection, month navigation, and transfer of the selected date |
| Rental packages | Package information, package selection, pricing, and transfer to the booking form |
| Booking | Contact fields, board quantities, participant limits, optional instructor, and total-price calculation |
| Simulated payment | Required fields, input validation, booking/payment integration, idempotency, and error handling |
| REST API | CRUD operations, status codes, validation, pagination, persistence, and error responses |
| Live chat | Message sending, display order, timestamps, and WebSocket behaviour |
| Location | Map loading, location details, and section layout |
| Accessibility | Selected checks using axe-core and keyboard interaction |
| Responsive behaviour | Desktop, tablet, and mobile viewport checks |

## Test design

I used the following test design techniques:

- Equivalence partitioning.
- Boundary value analysis.
- Positive and negative testing.
- Decision-based business-rule testing.
- Exploratory testing.
- API validation and persistence checks.
- Cross-feature regression testing.

Examples of covered business rules:

- Softboard rental price: **€40**.
- Hardboard rental price: **€55**.
- Performance board rental price: **€70**.
- Optional instructor: **€20 for one hour**.
- A booking supports a maximum of **10 participants**.
- A request containing 11 participants must be rejected.
- The booking total must reflect the selected boards and instructor option.
- Repeated payment requests with the same idempotency key must not create duplicate payments.
- Invalid client input must produce a controlled 4xx response rather than HTTP 500.

## Postman API testing

The Postman collection covers the Packs, Booking, and Payment API areas.

The collection includes:

- Positive CRUD scenarios.
- Required-field validation.
- Invalid input and boundary-value testing.
- Booking participant and price-calculation checks.
- Successful simulated payment scenarios.
- Missing and malformed `Idempotency-Key` validation.
- Repeated-request and duplicate-payment checks.
- Payment retrieval and pagination.
- Automatic preparation of test data.
- Collection variables and chained requests.
- Response status, structure, value, and persistence assertions.

The final collection run contained **421 automated assertions**.

## Regression testing

The final regression process combined several testing layers:

1. **Manual regression:** 150 key TestRail cases selected according to risk and business importance.
2. **API regression:** the Postman collection was executed against the updated backend.
3. **Automated support:** 177 AI-assisted Playwright UI and API checks were executed and analysed.
4. **Defect retesting:** 22 selected Jira defects were reviewed, with 19 confirmed fixed.
5. **Cross-feature verification:** Booking, Payment, package selection, price calculation, and related API persistence were checked together.

## Examples of defects identified

These examples describe findings discovered during testing and do not necessarily represent the current release status.

| Area | Finding | Expected behaviour |
| --- | --- | --- |
| API validation | A booking with 11 participants returned HTTP 500 | Reject the request with a controlled client-validation response |
| API persistence | A PATCH request returned HTTP 200, but a subsequent GET showed unchanged data | Persist and return the accepted update |
| Payment API | Overlong payment fields triggered HTTP 500 | Return HTTP 400 with a clear validation message |
| Payment API | A missing `Idempotency-Key` returned HTTP 500 | Return a controlled client error |
| Booking UI | Selecting a Softboard package could produce a €0 total | Calculate the total using the selected package |
| Booking UI | Package and instructor changes were not consistently reflected in the booking summary | Keep selected options and the total synchronised |
| Forecast and booking | A selected forecast date or package was not always transferred to the booking form | Preserve the user’s previous selection |
| Calendar | Past dates and invalid late times could be selected | Restrict selection according to the booking requirements |
| Performance | One home-page test run transferred approximately 147.5 MB in 46 requests | Optimise images and transferred resources for mobile loading |
| Chat | Message timestamps appeared in UTC | Display timestamps according to the agreed time-zone requirements |
| Location | The interactive map did not load | Display the configured location map correctly |

## Artifacts

| Folder | Contents |
| --- | --- |
| [`test-cases/`](test-cases/) | TestRail exports containing 359 test cases in total, including 6 Chat test cases, plus selected CSV exports |
| [`media/`](media/) | QA showcase video, preview GIF, and supporting visual materials |

Additional testing materials produced during the project included:

- Postman API collection and credential-free environment.
- Requirements Traceability Matrix covering 14 user stories.
- Manual and automated execution results.
- Jira defect reports with screenshots and technical evidence.
- AI-assisted Playwright regression results.

Project credentials, personal data, private Jira links, and other sensitive information are not included in the public repository.

## Repositories and links

- **Live application:** [surf-booking-ten.vercel.app](https://surf-booking-ten.vercel.app)
- **Frontend repository:** [7uckingbad/Surf_booking](https://github.com/7uckingbad/Surf_booking)
- **Backend repository:** [rmaksym1/surfing-booking-backend](https://github.com/rmaksym1/surfing-booking-backend)
- **Payment backend PR:** [PR #7 — Add payment for Booking API](https://github.com/rmaksym1/surfing-booking-backend/pull/7)
- **My QA portfolio:** [github.com/natalydemets/QA-Portfolio](https://github.com/natalydemets/QA-Portfolio)

## Contact

I am open to Manual QA Engineer opportunities, backend and API testing roles, and freelance QA projects.

More projects are available on my GitHub profile: [github.com/natalydemets](https://github.com/natalydemets).
