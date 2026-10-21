# Project Risks and Dependencies

In this document we describe the main risks of our diploma project, the Amateur Tennis Community Platform, and what we plan to do about them. We also list the things outside our team that the project depends on, such as developer accounts, services and people.

The list was made on 19 October 2026. We plan to look at it again at the end of each milestone, update the scores and add new risks if something comes up.

## How we rated the risks

For each risk we gave two scores from 1 to 3:

| Score | Probability | Impact |
|---|---|---|
| 1 – Low | Probably won't happen | Small delay, easy to fix |
| 2 – Medium | Could happen | We lose about a week or one feature gets weaker |
| 3 – High | Very likely to happen | A core feature, the demo or the deadline is in danger |

The risk score is probability × impact, so it goes from 1 to 9. We treat a score of 6 or more as a **major** risk. For major risks we also wrote a backup plan, in case the risk happens even after our mitigation.

Each risk has a person responsible for it. Timur works on the mobile app (Flutter) and Arlan on the backend (FastAPI). Some risks are about the whole project, so they belong to both of us.

## Risk register

| № | Risk | Type | Probability | Impact | Score | Responsible |
|---|---|---|---|---|---|---|
| 1 | The mobile app and the backend don't match on the API | Technical / integration | 2 | 3 | **6** | Both |
| 2 | The rating algorithm gives strange results | Technical | 2 | 3 | **6** | Arlan |
| 3 | Swiss-style pairings and automatic doubles pairs are harder than we expect | Technical | 2 | 3 | **6** | Arlan |
| 4 | Result confirmation and rating updates go wrong | Technical | 2 | 2 | 4 | Arlan |
| 5 | Setting up push notifications and the app stores takes a long time | Integration / external | 2 | 2 | 4 | Timur |
| 6 | Some technology decisions are still open, which may cause rework | Technical | 2 | 2 | 4 | Both |
| 7 | We don't have real match data to test the rating and matchmaking | Data access | 3 | 2 | **6** | Arlan |
| 8 | Personal data is stored or protected incorrectly | Data access / legal | 2 | 3 | **6** | Both |
| 9 | Our requirements are based on few interviews, and it is hard to find testers | Research | 2 | 2 | 4 | Both |
| 10 | The scope is too big for the time we have | Schedule | 3 | 3 | **9** | Both |
| 11 | Each part of the system has only one developer | Schedule | 2 | 3 | **6** | Both |
| 12 | Writing the thesis takes time away from development | Schedule | 2 | 2 | 4 | Both |
| 13 | We lose code or data | Technical | 1 | 3 | 3 | Both |

Risk matrix (numbers are risk IDs):

| Probability \ Impact | Low (1) | Medium (2) | High (3) |
|---|---|---|---|
| **High (3)** | | 7 | 10 |
| **Medium (2)** | | 4, 5, 6, 9, 12 | 1, 2, 3, 8, 11 |
| **Low (1)** | | | 13 |

We think the biggest risk is the scope (risk 10). Most of the other major risks are connected to the parts that make our app different from a normal tournament app: the rating, the pairings and the data we need to test them.

## Major risks and how we deal with them

### 1. The mobile app and the backend don't match on the API (score 6)

We work in parallel: Timur builds the app and Arlan builds the backend. If one of us changes an endpoint and the other doesn't know about it, the app stops working, and we might only find out when we connect everything near the deadline.

**Mitigation:** FastAPI creates the OpenAPI description automatically from the backend code, and we generate the Dart API client from it, so nobody has to write requests by hand. Every API change goes through a pull request that the other person checks. We also connect the app to the real backend at least once a week instead of working only with test data. Our main test is the full flow: register, join a tournament, submit a result, confirm it and see the new rating.

**If it happens anyway:** two weeks before the defence we freeze the API and only fix bugs after that.

### 2. The rating algorithm gives strange results (score 6)

We chose Glicko-2, but some details are not decided yet: how long a rating period is, what the starting rating is, how to count a doubles team, and how the internal rating turns into the NTRP-style level that players see. When a player has only a few matches, the rating can jump a lot. If the numbers look wrong, players won't trust them, and it will be hard to defend the main feature of the project.

**Mitigation:** the rating is a separate module with its own unit tests. One of the tests repeats the example from Glickman's Glicko-2 paper, where a player rated 1500 ends up at about 1464 after one win and two losses [1]. We will also simulate seasons with made-up players whose real strength we know, and check that the ratings put them in the right order (this is connected to risk 7). Players with an uncertain rating are shown as "provisional".

**If it happens anyway:** we switch to normal Elo. It is easier to explain and tune, and because the rating is a separate module, the other parts of the system don't need to change.

### 3. Swiss-style pairings and automatic doubles pairs are harder than we expect (score 6)

At first the rules look simple, but there are many special cases: players shouldn't meet twice, an odd number of players means someone gets a bye, there can be ties in the standings, and someone can leave in the middle of a tournament. Making balanced doubles pairs out of people who registered alone is also not trivial. These features are the main goal of the project, so we can't just remove them.

**Mitigation:** we start with simple rules: pair players by points, then by rating, never repeat an opponent, and give the bye to the lowest player who hasn't had one yet. Before writing the algorithm, we prepare test cases for small tournaments of 7, 8, 9 and 12 players. The organizer can also check and change the pairings before publishing them.

**If it happens anyway:** the app only suggests pairings, and the organizer confirms or edits them by hand. Doubles pairs are made in a simple way: the strongest player with the weakest one.

### 7. We don't have real match data to test the rating and matchmaking (score 6)

Our app is new, so there is no match history yet. The interviews gave us opinions, not results, and we have no agreement to import ratings from UTR or WTN. Without data it is hard to show that the rating and matchmaking really work.

**Mitigation:** we will write a small script that creates fake players with a hidden "real" level and simulates matches between them. We will also ask a local organizer for results of a past amateur tournament without names, and try to run at least one small test tournament with real players before the defence.

**If it happens anyway:** we test the algorithms only on simulated data and clearly write about this limitation in the thesis.

### 8. Personal data is stored or protected incorrectly (score 6)

The app stores names, contacts, match history and maybe an approximate location for search. In Kazakhstan, the Law on Personal Data (No. 94-V) says that personal data has to be stored on the territory of the country. In 2026 some laws changed the definition of personal data, and there is a draft decree that could relax the storage rule, but it is not adopted yet [6]. So the rules are changing, and if we choose hosting only by price, a test with real users could break the law. A data leak would also be a serious problem.

**Mitigation:** we only collect what the app really needs, and location is optional. Users agree to a short privacy notice when they sign up. Passwords are hashed, every request is checked with a JWT token, and organizers can only see their own tournaments. Until we choose hosting in Kazakhstan, we use only test accounts and generated data. We are not lawyers, so we will also ask our supervisor before inviting real users.

**If it happens anyway:** we run the test with a small group of people who agreed to it, on a server located in Kazakhstan, and show only generated data at the defence.

### 10. The scope is too big for the time we have (score 9)

The project includes accounts and profiles, singles and doubles tournaments, solo and team registration, automatic doubles pairs, scheduling, result confirmation, rating, player levels, statistics and matchmaking. This is a lot for two people who also have to write a thesis.

**Mitigation:** we use the MoSCoW method to decide what is most important:

- **Must have:** accounts, creating tournaments, singles and doubles registration, Swiss-style rounds, submitting and confirming results, rating updates.
- **Should have:** opponent and partner search, automatic doubles pairs, statistics and match history.
- **Could have:** notifications, offline cache, court search.

We work in two-week milestones in YouTrack and show each other a working demo at the end of each one. We try to finish features one at a time, so that every feature works all the way from the app to the database. We stop adding new features three or four weeks before the defence and use that time for testing, fixing bugs and writing.

**If it happens anyway:** we remove "could have" features first and then "should have" features, so that we always have a working version to show.

### 11. Each part of the system has only one developer (score 6)

Timur is the only one working on the app, and Arlan is the only one working on the backend. If one of us gets sick or is busy with exams, the other one can get stuck.

**Mitigation:** the app can run against a mock server made from the OpenAPI description, so mobile work doesn't stop if the backend is late. Each part of the repository has a README with instructions on how to run it. We review each other's pull requests, so we both understand the other part at least at a basic level. We write important decisions down in the repository, not only in chats.

**If it happens anyway:** the other person continues with a simpler version of the work, and we cut scope as described in risk 10.

## Other risks

**4. Result confirmation and rating updates go wrong (score 4).** Two players might enter different scores, someone might press "confirm" twice, or a dispute might be solved after other matches have already changed the ratings. To avoid this, the rating changes in the same database transaction as the result confirmation, and pressing "confirm" twice doesn't count the result twice. Disputed results don't count until the organizer solves the dispute. We also save the rating history, so ratings can be recalculated if an old result is corrected.

**5. Setting up push notifications and the app stores takes a long time (score 4).** To build the iOS app we need a Mac with Xcode. Push notifications and sending the iOS app to testers need the paid Apple Developer Program, which costs 99 USD per year [2][3]. A free account doesn't support push notifications [4]. On Google Play, new personal developer accounts (created after 13 November 2023) have to run a closed test with at least 12 testers for 14 days in a row before publishing [5]. Because of this, we will create the accounts early. Notifications are only a "could have" feature, and the "my next match" screen in the app gives the same information. At the defence we can show the app on Android (installed directly from an APK file) and on an emulator, so we don't need the stores.

**6. Some technology decisions are still open (score 4).** We still need to choose the Flutter state management library, the ORM and migration tool for the backend, and hosting. If we choose late, we may have to rewrite code. We will set a deadline for each decision and try each option on a small real example first. We will also lock library versions, so updates don't break the build unexpectedly.

**9. Our requirements are based on few interviews, and it is hard to find testers (score 4).** We interviewed only three players and no tournament organizers, even though half of the app is for organizers. One of the interviewees also said that an app like this is useless if nobody nearby uses it, so we need testers from the same area. We plan to interview two or three organizers or coaches before the tournament screens are finished, find testers through the club chat our interviewees use (this also helps with the 12 testers Google Play needs), and do short usability tests on the first working version.

**12. Writing the thesis takes time away from development (score 4).** The written part of the diploma and the defence presentation usually take more time than planned. We write the documentation during the project, not at the end. The comparisons, diagrams and this document are already in the repository. The last weeks before the defence are free from new features (see risk 10).

**13. We lose code or data (score 3).** A broken laptop or a mistake could cost us days of work. All code and documents are in a shared Git repository, and we push at least once a day. Test databases can be recreated from scripts. If we run a test with real users, the database is backed up automatically.

## External dependencies

| Dependency | Why we need it | What we do if there is a problem |
|---|---|---|
| Apple Developer Program (99 USD per year) [2][3] | Sending the iOS app to testers, push notifications on iOS [4] | Decide early if we pay for it. If not, we show iOS only on a simulator. |
| A Mac with Xcode | Building the iOS app | Use a team member's or the university's Mac, or a cloud build service |
| Google Play developer account | Publishing the Android app | Start the 14-day closed test early with testers from the club [5], or install the APK directly |
| Firebase Cloud Messaging and Apple Push Notification service | Push notifications (planned) | Use the "my next match" screen in the app instead |
| Email service | Account verification and password reset | Verify accounts manually during testing |
| Hosting with PostgreSQL | Running the backend for testing and the pilot | Use a local Docker setup for development, and choose hosting in Kazakhstan before real users join (risk 8) |
| Open-source libraries (Flutter, Drift, FastAPI, Pydantic) | The whole technology stack | Lock versions and update one library at a time |
| Clubs, organizers and players | Interviews, testing and a test tournament (risks 7 and 9) | Start with our interviewees' club, and ask a local amateur league if that doesn't work |
| Supervisor and university | Approving the scope, feedback, defence dates | Send documents to the supervisor as soon as each milestone is done |

Some of our own tasks also depend on each other:

1. The API has to be ready before the app can show real data.
2. The rating module has to be done before matchmaking, because matchmaking uses ratings.
3. Tournament registration comes before automatic doubles pairs and round pairings.
4. Result confirmation comes before rating updates, statistics and match history.
5. Hosting has to be chosen before any test with real users.

Because of this, we start with the backend part of the "must have" features. In the meantime, the mobile screens are built against the mock server.

## Sources

1. Mark E. Glickman, *Example of the Glicko-2 system*: http://www.glicko.net/glicko/glicko2.pdf
2. Apple Developer, *Membership details*: https://developer.apple.com/programs/whats-included/
3. Apple Developer, *Choosing a Membership*: https://developer.apple.com/support/compare-memberships/
4. Apple Developer Forums, discussion of the error "Personal development teams … do not support the Push Notifications capability": https://developer.apple.com/forums/thread/718388
5. Google Play Console Help, *App testing requirements for new personal developer accounts*: https://support.google.com/googleplay/android-developer/answer/14151465
6. AmCham Kazakhstan, *Data localization issue brief* (15 May 2026): https://amcham.kz/wp-content/uploads/2026/05/2026-05-15_AmCham_DataLocalization_Issue-Brief_ENG_v5.pdf
