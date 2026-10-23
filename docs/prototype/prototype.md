# Mobile Application UI/UX Prototype

## Project
Amateur Tennis Community Platform

## Figma Prototype
[View Interactive Prototype](https://www.figma.com/design/sE4gEJWR9tk9OnSE8iT5mX/ATC-prototype?node-id=0-1&t=FzblQIyH5qE6NiE9-1)

## Description
This prototype demonstrates the main user interfaces and workflows of the Amateur Tennis Community Platform mobile application.

The application allows amateur tennis players to discover tournaments, register for singles and doubles competitions, view their NTRP-style skill level, and track tournament match results.

A match result is submitted by one player and confirmed or disputed by the opponent. If the opponent disputes it, the tournament organizer resolves the dispute. Only confirmed or resolved results affect the internal rating (FR-03, FR-28, FR-29).

## Included Screens

| # | Screen | File |
|---|---|---|
| 1 | Login | [Login.png](<Login.png>) |
| 2 | Registration | [Registration.png](<Registration.png>) |
| 3 | Home | [Home.png](<Home.png>) |
| 4 | Tournaments | [Tournaments.png](<Tournaments.png>) |
| 5 | Tournament Details | [Tournaments Details.png](<Tournaments Details.png>) |
| 6 | Match Details (Player) | [Match Details.png](<Match Details.png>) |
| 7 | Match Details (Organizer) | [Match Details (Organizers).png](<Match Details (Organizers).png>) |
| 8 | Rating | [Rating.png](<Rating.png>) |
| 9 | Player Profile | [Player Profile.png](<Player Profile.png>) |
| 10 | Tournament Participants | [Tournament Participants.png](<Tournament Participants.png>) |

## Notes
- The prototype was created using Figma.
- The screens contain demonstration data.
- Players see an NTRP-style level (for example 3.5) with its band (for example Intermediate). The internal Glicko-2 rating is used by the system and is not shown (see the FR-01 clarification in `docs/requirements/interview-findings-requirements.md`). The level is NTRP-inspired, not an official USTA NTRP rating.
- In the first release, only confirmed or resolved tournament matches affect player ratings.
- Some interactions are represented as visual concepts and will be implemented during development.

## Pending updates in Figma

The current screens were made before the consistency review of 23 October 2026. They will be updated in milestone 2:

1. **Match Details (Player):** replace "Awaiting Organizer Approval" with "Waiting for your opponent to confirm", and show "Confirm" and "Dispute" buttons when the opponent opens the match.
2. **Match Details (Organizer):** replace "Approve / Reject" with a dispute-resolution view (enter the corrected score or void the match) that appears only for disputed matches.
3. **Home and Rating:** change "Updates after approved tournament results" and "calculated using tournament match results approved by organizers" to say that results are confirmed by the opponent.
4. **Level labels:** change "Estimated NTRP Level" and "E-NTRP Level" to "NTRP-style level"; show "Self-assessed" until the first confirmed match (FR-33), and the date of the last match next to "Provisional" (FR-04).
5. **Registration and Login:** add an "Area" field and a privacy-notice checkbox to Registration (FR-12, FR-34, NFR-09); change "Don't have an account? Sign In" to "Sign Up" on Login and add "Forgot password?" (FR-35).
6. **Home:** add a "My next match" card with the opponent, time and court (FR-10, NFR-11).
7. **Tournament Participants:** show rating status (Provisional) separately from registration status, and show teams for doubles tournaments.

Screens still to be designed: opponent and partner search (FR-05), result submission (FR-27), team invitation and its acceptance (FR-23), organizer screens for creating a tournament, managing registrations, doubles pairs, round pairings and the schedule, final standings (FR-31), and account settings with the privacy notice and account deletion (FR-37).

## Status
UI/UX prototype prepared for the first pre-defense.
