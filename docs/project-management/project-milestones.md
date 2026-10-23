# Project Milestones

In this document we describe the main milestones of our diploma project, the Amateur Tennis Community Platform. The plan shows how we want to move from research and planning, which we are finishing now for the first pre-defense, to a tested app and the final defense.

**About the dates.** The first pre-defense is on 24 October 2026. The other dates are approximate, because the university sets them, and we will update this plan when they are announced. For now we assumed that the second pre-defense is at the end of March or the start of April 2027, at the end of milestone 4, and that the final defense is around June 2027. We also left time for the winter exams and holidays.

## Overview

| № | Milestone | Approximate period | Main result |
|---|---|---|---|
| 1 | Research and planning (first pre-defense) | September – October 2026 | Requirements, comparisons, first diagrams and the project plan |
| 2 | Design and architecture | November 2026 | Database design, API specification, UI mockups, ready development environment |
| 3 | Core implementation | December 2026 – mid-February 2027 | A tournament can be run in the app from creation to final standings |
| 4 | Rating and matchmaking | mid-February – March 2027 | Glicko-2 ratings (with an Elo baseline), rating-based Swiss pairings, automatic doubles pairs, opponent search. Ends with the second pre-defense. |
| 5 | Testing and evaluation | April – mid-May 2027 | Tests, a pilot tournament with real players, evaluation of the rating |
| 6 | Final integration and documentation | mid-May – June 2027 | Final version of the app, thesis and presentation, final defense |

Inside each milestone we work in two-week sprints in YouTrack. At the end of each sprint we show each other what works. At the end of each milestone we also look at the risk register again (see *Project Risks and Dependencies*).

## 1. Research and planning — first pre-defense

**Period:** September – end of October 2026. **Status:** almost finished.

The goal of this milestone is to understand the problem, decide what we are going to build and plan the work. This is what we show at the first pre-defense.

What we have done:

- Wrote the critical literature review and the literature analysis table.
- Interviewed three amateur tennis players and analysed their answers.
- Wrote down the functional and non-functional requirements, their priorities and acceptance criteria.
- Compared existing systems (UTR, Playtomic, Global Tennis Network, ITF World Tennis Number and Tennis League TS).
- Compared technology alternatives and chose Flutter, FastAPI as a modular monolith, PostgreSQL and Glicko-2 (with Drift for the optional offline cache).
- Chose the Swiss-style system as the first tournament format.
- Made the system context diagram, the use case diagram and a first draft of the component diagram.
- Made the first Figma prototype of the key screens.
- Wrote the verification and evaluation plan, the risk register and this milestone plan.
- Set up the repository and the YouTrack board.

**Done when:** all documents are in the repository and the first pre-defense presentation is ready.

## 2. Design and architecture

**Period:** November 2026 (about 4 weeks).

In this milestone we turn the requirements and the draft diagrams into a design that we can actually start coding from.

Main tasks:

- Design the database and draw an ER diagram (users, tournaments, registrations, teams, matches, results, ratings, rating history).
- Write the first version of the API specification (OpenAPI) for the main flows, so that Timur can start the app with a mock server (Arlan, Timur).
- Update the Figma prototype so it shows opponent confirmation of results, and add the screens that are still missing: opponent and partner search, result submission and confirmation, team invitations, the organizer screens and "my next match" (Timur).
- Make the remaining technology decisions: the state management library in Flutter, the ORM and migration tool on the backend, and where to host the backend (see risks 6 and 8).
- Set up the development environment: the backend and database in Docker, the module structure of the backend, the Flutter project and a simple CI that runs the tests.
- Interview two or three tournament organizers or coaches, because we haven't talked to any organizers yet (risk 9).
- Update the component diagram after these decisions.

**Done when:** the ER diagram, the API specification and the mockups are reviewed by both of us, and both the app and the backend can be started locally by following the README.

## 3. Core implementation

**Period:** December 2026 – mid-February 2027 (about 10 weeks, including a break of 2–3 weeks for winter exams and holidays).

In this milestone we build the "must have" features (see the requirement priorities), except the ones that depend on the rating: rating updates, rating-based pairings, automatic doubles pairs and opponent search come in milestone 4. At the end, a whole tournament should work in the app, even if the pairings are still simple.

Backend (Arlan):

- Registration with privacy-notice consent, login with JWT sessions that are revoked on sign-out, account deletion, and player profiles with a self-assessed starting level.
- Creating tournaments in singles and doubles formats.
- Registration for tournaments, alone or as a team with a partner, and managing registrations for organizers.
- Simple Swiss-style rounds that pair players by points only (pairing by rating comes in milestone 4).
- Match schedule, result submission, confirmation by the opponent, disputes and their resolution by the organizer, and the audit trail of result changes.
- Final standings.

Mobile app (Timur):

- App structure, navigation and the API client generated from the OpenAPI description.
- Login, registration and profile screens.
- Tournament list and tournament page with schedule, draws and results.
- Organizer screens for creating a tournament and managing registrations.
- Screens for entering and confirming results.

**Done when:** we can create a small test tournament with 8 players, register them, play all rounds, enter and confirm the results and see the final standings, all from the app with the real backend.

## 4. Rating and matchmaking

**Period:** mid-February – end of March 2027 (about 6 weeks). It ends with the second pre-defense.

This milestone is about the main idea of our project: ratings based on match results, and matching players and teams by level.

Main tasks:

- Implement the Glicko-2 rating module with unit tests, including the example from Glickman's paper. Ratings are kept separately for singles and doubles.
- Implement plain Elo behind the same interface. It is the fallback if Glicko-2 causes problems, and the baseline we compare Glicko-2 with in milestone 5.
- Decide the starting ratings, how doubles results update both partners, and how the internal rating turns into the NTRP-style level players see. Players with an uncertain rating are shown as "provisional".
- Process each confirmed match as soon as it is confirmed, as its own rating period, and increase the rating deviation with the time since a player's last match. Check with the simulation script whether this works well enough, because Glicko-2 is designed for rating periods with several games.
- Update ratings when a result is confirmed, in the same database transaction, and save the rating history. If an old result is corrected, recalculate the affected ratings by replaying the confirmed results in order.
- Write a script that creates fake players and simulates matches, so we can check that the rating works before we have real data (risk 7).
- Improve the Swiss-style pairings: by points and then by rating, no repeated opponents, and byes for an odd number of players.
- Form balanced doubles pairs automatically from players who registered alone.
- Opponent and partner search by level.
- Rating, statistics and match history screens in the app.

**Done when:** confirmed results change the ratings correctly, the app generates pairings and doubles pairs for test tournaments of 7–12 players without mistakes, and search shows players of a similar level. We show this at the second pre-defense.

If this milestone takes longer than planned, we use the backup plans from the risk register: plain Elo instead of Glicko-2, and pairings that the organizer confirms by hand (risks 2 and 3).

## 5. Testing and evaluation

**Period:** April – mid-May 2027 (about 6 weeks).

In this milestone we check how well the app works, both technically and for real users.

Main tasks:

- Write more unit and integration tests and an end-to-end test of the main flow: register, join a tournament, submit a result, confirm it and see the new rating.
- Run a small pilot tournament with real players, starting with the club of the players we interviewed (risk 9).
- Do short usability tests with players and at least one organizer and write down the problems they have.
- Evaluate the rating as described in the Verification and Evaluation Plan: compare Glicko-2 and Elo with the players' self-assessed starting levels, on simulated data and on the results from the pilot tournament.
- Fix bugs and improve the screens based on the feedback.
- Add "could have" features (push notifications, offline cache) only if all "must have" and "should have" features are finished.

**Done when:** the test results and user feedback are written down, and there are no critical bugs left in the main flows.

## 6. Final integration and documentation

**Period:** mid-May – June 2027, until the final defense.

At the start of this milestone we stop adding new features (feature freeze), about 3–4 weeks before the defense, as planned in the risk register (risk 10). After that we only fix bugs, finish the integration and work on the thesis.

Main tasks:

- Deploy the backend to the chosen hosting and prepare the final Android build (APK). The iOS version is shown on a simulator if needed (risk 5).
- Update all diagrams so they match the finished system.
- Finish the thesis: analysis, design, implementation, testing and evaluation. We start writing the first chapters already during milestones 4 and 5, so that not everything is left for the end (risk 12).
- Prepare the defense presentation, plus a short demo video in case something goes wrong during the live demo.
- Rehearse the defense together.

**Done when:** the thesis is submitted, the app works on a real device with the deployed backend, and the presentation is ready for the final defense.

## Dependencies between milestones

- Milestone 2 has to finish before serious coding starts, because the app and the backend both depend on the API specification and the database design.
- In milestone 3 the backend part goes first. Until it is ready, the app works against the mock server.
- Milestone 4 needs confirmed results from milestone 3, because ratings are calculated from them.
- The pilot tournament in milestone 5 needs the rating and pairings from milestone 4, and hosting that is allowed for real personal data (risk 8).
- If one milestone runs late, we cut "could have" and then "should have" features instead of moving the final defense.
