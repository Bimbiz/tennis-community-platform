# Project Proposal and Scope

**Project title:** Development of a Mobile Application for the Amateur Tennis Community with Automatic Rating Calculation and Matching of Pairs  
**Project:** Amateur Tennis Community Platform  
**Educational program:** Software Engineering  
**Team:** Timur Bizinskiy (SE-2412) — Mobile Development; Arlan Tulegenov (SE-2429) — Backend Development  
**Academic supervisor:** Zhibek Sarsenova, Senior Lecturer  
**Document status:** Draft v0.1 — pending team and supervisor review  

## 1. Project Overview

The project proposes a cross-platform mobile application for amateur tennis players and tournament organizers. It will provide a unified way to publish tournaments, register players, form singles matchups and doubles teams, record match outcomes, and maintain automatically updated player ratings. Tournament-specific rules and scheduling will be handled on the backend, while players and organizers will interact through the mobile client.

## 2. Problem Statement

Amateur tennis activities are often coordinated through messaging groups and other informal channels. As a result, information about available tournaments and participants can become fragmented, organizer workflows require manual coordination, and players may struggle to find suitably matched competition. Skill levels can also be difficult to compare consistently when participation histories differ.

The proposed system seeks to make tournament participation and organization more structured, and to investigate how match-based rating calculations can support more balanced matchmaking. These are preliminary problem assumptions to be checked through interviews with potential users and comparison with existing platforms.

## 3. Target Users

- **Amateur tennis players:** discover and join tournaments, register individually or with a doubles partner, view scheduled matches, confirm results, and track their progress.
- **Tournament organizers:** create tournaments, manage registration and participants, initiate team and match formation, and oversee results.
- **Local tennis communities and clubs:** potential users of a shared tournament-management workflow.

A single account may participate as a player and organize tournaments, subject to authorization rules.

## 4. Project Aim

To design, implement, and evaluate a cross-platform system that supports amateur tennis tournament management, rating-informed opponent and partner matching, and automated player rating updates based on confirmed match results.

## 5. Project Objectives

1. **Investigate user needs and existing solutions:** collect feedback from potential players and organizers, review relevant literature, and compare current tennis-related platforms.
2. **Specify and design the system:** define verifiable functional and non-functional requirements; design the client–server architecture, core data entities, API contracts, and mobile user flows.
3. **Develop the tournament workflow:** implement user profiles, tournament creation and registration, singles participation, doubles team registration/formation, and match scheduling for an agreed initial competition system.
4. **Develop and assess the rating mechanism:** implement a selected internal rating method (Elo or Glicko-2), explore its conversion into a clearly labelled NTRP-inspired displayed level, and evaluate matchmaking and rating behaviour using defined metrics.
5. **Integrate and verify the application:** connect the Flutter client with the FastAPI backend and carry out functional, integration, usability, and algorithmic testing.

## 6. Proposed Solution and Technical Approach

- **Mobile client:** Flutter / Dart; player and organizer interfaces, navigation, client-side validation, API integration, and error handling.
- **Backend:** Python / FastAPI in a modular monolithic architecture; authentication, tournament lifecycle, registrations, match and team formation, results, and rating calculations.
- **Communication:** REST/JSON with a documented OpenAPI contract.
- **Data storage:** a relational database, with PostgreSQL currently under evaluation; optional local mobile caching is also under evaluation.
- **Rating:** an internal Elo or Glicko-2 score; the public-facing NTRP-inspired category will be derived through a conversion approach that must be justified and tested, not presented as an official USTA NTRP rating.

Final technology choices will be supported by the separate Technology Comparison document.

## 7. Project Scope

### 7.1 Core Scope (planned first working release)

- Account registration, login, and basic player profiles.
- Initial self-assessment of playing level, clearly distinguished from the calculated rating.
- Tournament creation, publishing, registration windows, and participant management.
- **Singles and Doubles** as participation formats.
- Doubles registration with an existing partner (subject to both players' confirmation) or individual registration for automatic partner formation before tournament start.
- Generation and presentation of matches for **one initially selected competition system**; the team will confirm which system is delivered first during design.
- Match result submission, confirmation, and history.
- Internal rating updates after confirmed results, with a user-friendly displayed level.
- Basic organizer and player screens, including loading, empty, and error states.

### 7.2 Planned Extensions (subject to time and validation)

- Additional competition systems from the candidate set:Single Elimination, Double Elimination, Swiss, Round Robin / Box Leagues, and King of the Court / Ladder (TBD). 
These are candidates, not a commitment to deliver every format. The rules and classification of King of the Court / Ladder will be determined during requirements analysis.
- Push notifications and real-time updates.
- Expanded statistics, visualizations, maps, and location-based discovery.
- More advanced tournament administration and organizer tools.

### 7.3 Out of Scope for the Initial Release

- Court booking, payment processing, and ticketing.
- Professional federation certification or issuance of **official** NTRP ratings.
- A separate web administration application.
- Full support for all proposed competition systems in the first release.
- Large-scale production deployment or guarantees of commercial-grade capacity.

## 8. Key Business Rules and Assumptions

- A tournament organizer selects Singles or Doubles and defines applicable registration rules.
- In Doubles, confirmed premade teams remain intact; automatic pairing applies only to unpaired participants.
- Doubles teams are formed before tournament play begins and remain fixed during that tournament under the initial rules.
- A player must not occupy more than one team position in the same tournament.
- Confirmed match results update the internal player rating exactly once; disputes and reversals need explicit handling.
- A player's initial displayed self-assessment is not treated as a verified competitive level.
- The method for rating doubles outcomes, initial rating uncertainty, and public-rating conversion remains subject to research and testing.

## 9. Expected Outcomes and Deliverables

1. A documented requirements specification and project scope, supported by relevant user evidence and literature.
2. Architectural diagrams, a documented API contract, and an interactive mobile UX prototype.
3. Source code for a functioning Flutter client and FastAPI backend implementing the agreed core workflow.
4. An implemented and evaluated internal rating mechanism, together with a clearly described method for presenting a user-facing skill category.
5. Test cases, evaluation results, known limitations, and a traceable GitHub/YouTrack development history showing each team member's contributions.

## 10. Engineering Complexity

The project combines multiple interacting engineering problems: authorization across player and organizer workflows; modelling tournaments, registrations, teams, matches, and results; preserving data integrity when multiple players register or results are confirmed; algorithmic team/match formation and rating updates; and robust mobile–server integration. These components require coordinated architectural decisions, testable requirements, and verification beyond a static user-interface prototype.

## 11. Validation and Scope Control

The team will validate assumptions with potential users and the supervisor. A baseline implementation will be assessed through functional acceptance tests, integration checks, selected usability scenarios, and rating/matchmaking metrics defined in the Verification and Evaluation Plan. The exact competition system for the first implementation, database choice, algorithm, and implementation milestones will be finalized after a joint scope review.

**Pre-defence note:** The October 24 milestone requires project analysis, architecture, prototype materials, documentation, and development planning; a complete application is not required at that stage.
