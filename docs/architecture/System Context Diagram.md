# System Context Diagram

![System Context Diagram](system-context.png)

The diagram shows the Amateur Tennis Community Platform as a single system, the people who use it, and the external services it depends on. The dashed blue frame marks the system boundary. Everything inside it is built by our team, and everything outside it is a person or a third-party service.

Inside the boundary we show only the two main parts, so it's clear where the mobile app sits:

- **Mobile Application.** The Flutter app for Android and iOS that players and organizers use. It keeps a local copy of schedules and results.
- **Backend Server.** The FastAPI application with its PostgreSQL database. It handles accounts, tournaments, matches, result confirmation and rating calculation.

The two parts talk to each other through a REST/JSON API over HTTPS.

## Actors

- **Player.** An amateur tennis player who registers, joins tournaments (alone or as a premade team), submits and confirms match results, and follows their schedule, rating, level and match history.
- **Tournament Organizer.** A person who runs tournaments for a club or community: creates tournaments, manages registrations and schedules, and enters or resolves results. The organizer sees registration lists, automatically generated doubles pairs, draws and results.

## External services

Both external services are shown with dashed borders because notification services are subject to scope prioritization (see the project README). They are not required for the first version.

- **Push Notification Service.** Firebase Cloud Messaging for Android and Apple Push Notification service for iOS. The backend sends notification requests, and the service delivers match reminders and result confirmation requests to the app.
- **Email Service.** A transactional email provider used for account verification and password reset.

## Main information flows

| From | To | Information |
|---|---|---|
| Player | Mobile app | Registration, tournament sign-ups (solo or team), match results and confirmations |
| Mobile app | Player | Schedules, draws, results, rating, level and match history |
| Organizer | Mobile app | New tournaments, registration and schedule management, entered or resolved results |
| Mobile app | Organizer | Registration lists, generated doubles pairs, draws and results |
| Mobile app | Backend | REST/JSON requests and responses over HTTPS |
| Backend | Push service | Notification requests |
| Push service | Mobile app | Push notifications |
| Backend | Email service | Verification and password-reset emails |

## Files

- `system-context.drawio`: editable source. Open it at [diagrams.net](https://app.diagrams.net) or with the Draw.io Integration extension in VS Code.
- `system-context.png`: exported image for documents and slides.
- `system-context.svg`: exported vector image. It also contains a copy of the diagram, so it can be opened and edited in diagrams.net too.

After editing the `.drawio` file, export it again (File → Export as → PNG / SVG) so the images stay in sync.
