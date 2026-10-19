# Verification and Evaluation Plan

**Project:** Amateur Tennis Community Platform  
**Task:** ATC-17  
**Status:** Draft v0.1 — plan only; no evaluation results collected

## 1. Purpose and source documents

This plan describes how the team will verify functional and non-functional requirements and evaluate whether dynamic ratings and skill-based matching help amateur tennis players. It does not claim the application has been built or tested.

Requirement identifiers refer to `interview-findings-requirements.md` (FR-01–FR-15), `functional-requirements-addition.md` (FR-16–FR-33), and `non-functional-requirements.md` (NFR-01–NFR-18). The `requirement-priorities-and-acceptance-criteria.md` document supplies the agreed draft acceptance checks. Priorities and original wording are not modified here. F1–F15 below refer to interview findings, not functional requirements.

## 2. Functional verification

| Requirements | Proposed method | Observable acceptance evidence |
|---|---|---|
| FR-12, FR-16–FR-18, FR-33 | End-to-end registration, valid/invalid login, logout, edit own/other profile and initial self-assessment tests. | Eligible operations succeed; unauthorized edits and invalid credentials fail; starting assessment is visibly distinguished from calculated rating. |
| FR-01–FR-04, FR-30 | Rating unit tests with known match outcomes, confirmation state integration tests and duplicate-request tests. | The selected documented rating method produces reproducible values; unconfirmed results do not change ratings; a confirmed result updates ratings at most once. FR-04 is Should. |
| FR-05–FR-08 | Search over fixture users with varied ratings; optional availability/location tests; doubles suggestion tests. | Level filters return matching players or a clear empty state. Optional Should features follow their ATC-12 checks if implemented. |
| FR-19–FR-22, FR-32 | End-to-end tournament publication, browsing, registration, duplicate/eligibility rejection, closing registration and organizer authorization tests. | Correct tournaments appear; authorized organizers manage registration; closed or duplicate entries are rejected. |
| FR-23–FR-24 | Doubles team invitation and automated pairing tests with odd/even numbers, existing teams and duplicate attempts. | Premade teams require both players' consent; each player appears in at most one team; unpaired remainder is reported. |
| FR-25–FR-26, FR-31 | Generate competition draw using the **first approved tournament format** (TBD), inspect participants, rounds, schedule updates and final standings. | Generated rounds respect the approved format's rules; schedule and standings are displayed accurately. |
| FR-03, FR-27–FR-29 | Submit scores, confirm or dispute as authorized opponent, reject unrelated users and record organizer resolution. | Pending scores do not affect ratings; confirmation/dispute states and permissions work; resolution is recorded. Rating treatment of organizer-resolved scores is TBD. |
| FR-09–FR-11, FR-13–FR-15 | Manual and automated checks for any delivered Should/Could features (tournament information, notifications, history, divisions, court availability, streamlined registration). | Each delivered feature satisfies its ATC-12 acceptance check; deferred features remain explicitly marked deferred, not passed. |

**Evidence traceability:** F1–F5 support rating and self-assessment requirements; F6 and F9–F11 support opponent search and matching; F7–F8 support tournament visibility; F12 supports simple onboarding. These references originate in `interview-findings-requirements.md`. Organizer-oriented requirements mainly originate in the Project Proposal and Use Case Diagram: the three completed interviews were with players, not organizers.

## 3. Non-functional verification

| NFR IDs | Measurement / test conditions | Proposed acceptance criteria |
|---|---|---|
| NFR-01 | API load test of profile, tournament listing and match history reads; 30 concurrent simulated users for 10 minutes. | ≥95% of successful requests complete within 1.5 seconds. |
| NFR-02 | API load test of registration, result confirmation and rating operations at the same concurrency/duration. | ≥95% of successful operations complete within 3 seconds; failures reported separately. |
| NFR-03 | Simulate delayed responses while observing mobile screens. | Progress feedback visible within 1 second (Should). |
| NFR-04–NFR-06 | API authorization and invalid-input tests; inspect TLS, credential storage, logs and tracked repository files; replay confirmation requests. | Protected actions reject unauthorized users; no plaintext stored passwords or committed secrets; duplicates do not change ratings twice. |
| NFR-07–NFR-09 | Audit mandatory/optional profile fields; inspect contact/location visibility and privacy notice. | Only justified fields are mandatory; private information is hidden by default; notice exists if Should NFR-09 is delivered. |
| NFR-10–NFR-11 | Moderated usability test with at least five participants: registration and skill assessment; find a tournament; locate the next match. | At least four of five finish each required task without assistance; times and errors recorded. |
| NFR-12 | Screen inspection on at least one Android and one iOS device/simulator at up to 200% text size. | Core tasks remain usable (Should). |
| NFR-13–NFR-14 | Inject connection/transaction failures during registration and result confirmation; retry and inspect persisted state. | No partial rating updates or false success messages; input loss is handled visibly. |
| NFR-15 | Restore test database backup and compare expected data. | Representative users, tournaments, results and ratings recover consistently (Should). |
| NFR-16–NFR-17 | Both team members follow setup instructions and run automated tests for rating, tournament rules and permissions. | Setup reproducible; relevant regression tests execute with recorded outcomes. |
| NFR-18 | Mixed-operation load test with 30 concurrent simulated users over 10 minutes. | ≥99% successful valid requests without critical corruption (Should). |

All numerical limits are existing **proposed NFR thresholds**, not achieved metrics. Before testing, document backend hardware/CPU/RAM, database, dataset size, deployment, mobile devices, network, tools, software version/commit and workload mix.

## 4. Rating evaluation: organizer baseline, Elo and Glicko-2

### 4.1 Approaches

1. **Organizer-assigned starting level — baseline:** an organizer/coach estimates each player's ability *before* test matches. Hold this value fixed throughout the evaluation period. This is a **research baseline**, not a requirement that organizers assign levels in the app.
2. **Player self-assessment — optional onboarding baseline:** use the initial self-reported level, held constant. This corresponds to the planned onboarding and should be reported separately from organizer estimates.
3. **Elo:** dynamic ratings updated only using eligible earlier confirmed matches; the K-factor and initialization rules are specified before final evaluation.
4. **Glicko-2:** dynamic rating, rating deviation and volatility; declare rating period, inactivity handling, initialization and tuning before final evaluation.

If organizer assessments are **not available**, do not invent them: mark this baseline *unavailable*, obtain them prospectively if possible, and present any self-assessment comparison as a separate baseline rather than relabeling it.

### 4.2 Data and fair comparison

- Prefer consented, anonymized chronological amateur match data with player IDs, date/order, result, Singles/Doubles designation and **pre-match** organizer level where available. Synthetic data may verify algorithms but **cannot demonstrate real-world predictive advantage**.
- Sort matches chronologically; for each match, predict first, then apply its outcome to dynamic ratings. No model may use results from future matches to initialize or tune itself.
- Use a chronological training/validation window for tuning and calibration and a later held-out test window for reporting. Compare all methods on **the same eligible test matches**.
- For categorical organizer/self-assessed levels, derive win-probability predictions using a documented conversion calibrated only on training data. Do not treat NTRP-inspired levels as official NTRP.
- Evaluate Singles primarily. Doubles should be evaluated separately after team-strength aggregation and rating updates are formally specified.
- Record match counts, exclusions, new/inactive-player definitions, data permission, model parameters and uncertainty; distinguish unavailable baselines from weak results.

### 4.3 Outcome metrics

| Metric | How measured | Interpretation |
|---|---|---|
| Winner prediction accuracy | Correct predicted winners / evaluated matches, with a predeclared tie rule. | Intuitive, but sensitive to class balance. |
| Brier score | Mean squared difference between predicted win probability and actual binary result. | Probability error; lower is better. |
| Log loss | Mean negative log likelihood of the actual outcomes; probabilities clipped to a declared epsilon. | Penalizes confident incorrect predictions; lower is better. |
| Calibration | Observed win rate versus mean prediction within predeclared probability bins; include bin counts. | Indicates whether reported probabilities are trustworthy. |
| Cold-start analysis | Repeat metrics for players with few earlier matches (threshold fixed before test). | Tests usefulness for new players. |
| Inactivity analysis | Repeat metrics by time since a player's previous result. | Tests robustness to infrequent play. |
| Matching balance | Distribution of absolute deviations from a 50% pre-match predicted win chance for proposed pairings. | Predicted fairness only; not proof of user satisfaction. |
| Doubles balance (if applicable) | Distribution of rating-derived strength gaps between formed teams under approved doubles rules. | Assesses balanced-team objective; requires documented team-rating method. |

Where data allow, report confidence intervals and paired differences using the same held-out matches. If data are too sparse, report descriptive results without claiming that one algorithm is superior.

## 5. Tournament, matchmaking and usability evaluation

**Opponent matching:** use preconstructed player fixtures with different ratings and optional availability/location data to verify that suggested opponents respect eligibility and filters (FR-05–FR-07). During user tests, record whether a user can identify a suitable opponent and how long it takes.

**Doubles formation:** use repeatable scenarios with premade teams, odd solo-player counts and diverse ratings. Check partner consent, absence of duplicate registrations and identification of unmatched players (FR-23/FR-24). Where feasible compare predicted team-rating imbalance with a simple random-pairing baseline using a fixed seed, *without claiming actual competitive balance before matches are played*.

**Tournament workflow:** scripted end-to-end test of organizer publishing → participant registration → team formation → draw/matches → result submission and opponent confirmation → final standings. Check unauthorized actions and state transitions.

**Usability:** at least five participants attempt onboarding, opponent search, tournament discovery and match lookup. Record completion, assistance, errors and elapsed time. Add organizer feedback if possible: original interviews did not include organizers.

## 6. Measurement evidence and reporting

For every executed test retain: test ID, linked FR/NFR, dataset or fixture, expected outcome, observed outcome, pass/fail/not-run/deferred status, environment, date and software commit. Store automated test outputs, performance logs, anonymized user observations and screenshots in the repository documentation or test folders. Link defects to YouTrack.

The later evaluation report should distinguish: requirements **passed**, **failed**, **not run**, or **deferred**; show measured NFR values and conditions; provide data source, model settings and held-out metrics for each available rating baseline; record shortcomings and unresolved decisions. No test is marked passed solely because a procedure is documented.

## 7. Open decisions and limitations

- The first supported competition format remains **TBD**; its detailed progression test cases cannot be finalized yet.
- Glicko-2 is recommended in the technology comparison but the team's final production choice and rating-period definition remain subject to approval.
- Organizer-assigned ratings are a baseline **only if genuinely collected before matches**; the application currently proposes player self-assessment for onboarding.
- Doubles rating/aggregation, displayed skill-band conversion, and whether organizer-resolved disputed outcomes affect rating remain **TBD**.
- Initial field evidence consists of **three player interviews**; there were no organizer interviews. Further evaluation with organizers is desirable.
- This document is a **future verification and evaluation plan**, not evidence of tests already completed. Measurements, predictive scores and application outcomes **have not yet been collected**.

## 8. Responsibilities and milestones

| Stage | Activity | Responsibility | Evidence |
|---|---|---|---|
| Pre-defence planning | Review acceptance tests, metrics and feasibility; approve baselines and unresolved decisions. | Joint (Timur, Arlan; supervisor review) | Approved plan and requirements traceability. |
| Implementation | Write repeatable tests for API, data integrity, algorithm and mobile workflows. | Arlan: backend/rating; Timur: mobile/UX | Test cases and CI/local test logs. |
| Evaluation | Execute functional, NFR, usability and rating comparisons under recorded conditions. | Joint | Logs, measurements and anonymized observations. |
| Final report | State fulfilled requirements, results, limitations and deviations. | Joint | Final evaluation chapter. |

**October 24 pre-defence:** only this plan and other required analysis materials are expected; the table above describes later work, not existing results.
