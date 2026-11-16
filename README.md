# Surf Booking Landing — QA Case Study

**Manual UI and API testing for an educational team web application.**

**Author:** Natalie Demets  
**Role:** Manual QA Engineer / TestRail Administrator

Surf Booking Landing lets users explore a surf forecast, choose rental equipment, configure a booking, and complete a simulated payment. The application also includes a live chat and a location map.

## Project overview

| Area | Details |
| --- | --- |
| Project type | Educational team project |
| Team | QA, Frontend Developer, Backend Developer, Project Manager, Business Analyst, Designer |
| Process | Agile sprints; defect tracking in Jira |
| Frontend | React and TypeScript |
| Backend | Java Spring Boot REST API |
| Other components | WebSocket chat; PostgreSQL |
| Testing tools | TestRail, Postman, Jira, Chrome DevTools |

This repository presents my QA contribution. The application source code is maintained by the development team.

## My responsibilities

- Analyze requirements and Figma designs, identify unclear behavior, and discuss it with the team.
- Design test cases and checklists for UI flows and API endpoints.
- Organize test documentation and test runs as the TestRail administrator.
- Test booking calculations, field validation, package selection, and simulated payment flows.
- Check REST API responses, validation, and data persistence using Postman.
- Report defects in Jira with reproduction steps, expected and actual results, and supporting evidence.
- Retest fixes and perform regression testing across related features.

## Testing scope

| Feature | Focus |
| --- | --- |
| Home and navigation | Links, buttons, section navigation, layout |
| Forecast and calendar | Date selection and navigation |
| Rental packages | Package selection and transfer to the booking form |
| Booking | Contact fields, board quantities, participant limits, optional instructor, total price |
| Simulated payment | Request validation, booking/payment integration, error handling |
| Live chat | Message display and timestamps |
| Location | Map and location section |

## Test design

I used equivalence partitioning, boundary value analysis, positive and negative scenarios, and exploratory testing.

Examples of business rules covered:

- Softboard: **€40**; Hardboard: **€55**; Performance: **€70**.
- Optional instructor: **€20 for one hour**.
- A booking supports a maximum of **10 participants**; 11 must be rejected.
- The booking total must reflect the selected boards and instructor option.

## Examples of defects identified

These examples describe findings during testing, not the current release status.

| Area | Finding | Expected behavior |
| --- | --- | --- |
| API validation | A booking with 11 participants returned HTTP 500 | Reject the request with a client validation error |
| API persistence | A PATCH request returned HTTP 200, but a subsequent GET showed unchanged data | Persist the accepted update |
| Payment API | Overlong field values triggered HTTP 500 | Return a controlled validation response |
| Booking UI | Selecting a Softboard package could produce a €0 total | Calculate the total from the selected package |
| Booking UI | Package changes or the instructor option were not consistently reflected in the booking | Keep booking selections and the total synchronized |
| Chat | Timestamps appeared in UTC | Display timestamps according to the agreed time-zone requirements |

## Supporting artifacts

The repository currently contains this case study. Original testing artifacts will be added as they are prepared for public sharing:

- TestRail test cases and test run exports.
- UI checklists.
- Bug reports with screenshots.
- Postman collection and an environment without credentials.
- Test execution summary.

## Portfolio

See my other testing projects in [QA Portfolio](https://github.com/natalydemets/QA-Portfolio).
