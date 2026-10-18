# Requirements Priorities and Acceptance Criteria

**Project:** Amateur Tennis Community Platform  
**Task:** ATC-12 - Define Requirement Priorities and Acceptance Criteria  
**Status:** Draft for team and supervisor review  
**Coverage:** FR-01–FR-33 and NFR-01–NFR-18

## Purpose and source of truth

This matrix consolidates **existing** requirement IDs, priorities, and verifiable acceptance checks without renumbering or rewriting the requirements maintained in the source documents:

- `interview-findings-requirements.md`: FR-01–FR-15 (Arlan; priority and interview evidence preserved).
- `functional-requirements-addition.md`: FR-16–FR-33 (additional functional requirements; the file was previously named `functional-requirements-addendum.md`).
- `non-functional-requirements.md`: NFR-01–NFR-18 (proposed quality thresholds and checks).
- `Usecase Diagram.md`: UC identifiers; `project-proposal.md`: scope baseline.

The wording of the authoritative requirement is maintained in its source file; the rows below describe **how compliance will be verified**. Reviewers should use the ID to locate the full requirement. No requirement is marked implemented or tested merely because its acceptance check has been defined.

## Priority scheme

- **Must (M):** required by the current documented baseline for the proposed first release.
- **Should (S):** desirable for a usable release, but may be deferred if capacity is limited.
- **Could (C):** optional extension, not required for acceptance of the initial release.

Priorities have been copied **without changing** the source documents. The team must approve any changes; this matrix does not silently upgrade a Should or Could to Must. Each requirement, including optional ones, has an acceptance check for possible later verification.

## A. Interview-derived functional requirements (FR-01–FR-15)

| ID | Priority | Acceptance criterion (observable outcome) | Evidence / source |
|---|---|---|---|
| FR-01 | Must | A player profile displays a numeric rating and corresponding labelled level band. | F1, F5; `interview-findings-requirements.md` |
| FR-02 | Must | After a confirmed match, the player rating changes according to the selected documented method; changing an initial self-assessment alone does not count as a confirmed match result. | F2, F3, F4, F5; `interview-findings-requirements.md` |
| FR-03 | Must | A submitted result remains pending and does not affect the rating until an eligible opponent confirms it. | F2; `interview-findings-requirements.md` |
| FR-04 | Should | New or inactive players display a provisional indicator and the date of their last recorded match. | F3, F15; `interview-findings-requirements.md` |
| FR-05 | Must | A search with a chosen level range returns only players within that range (or a clearly labelled empty state). | F1, F6; `interview-findings-requirements.md` |
| FR-06 | Should | An availability filter restricts results to the selected time window; a published play-now/weekend request can be found. | F6, F10; `interview-findings-requirements.md` |
| FR-07 | Should | Selecting an area or distance filter restricts visible results accordingly when a player has opted to share the necessary location. | F6, F11; `interview-findings-requirements.md` |
| FR-08 | Should | A player can view previous doubles partners and receive a proposed pairing generated from recorded levels. | F9; `interview-findings-requirements.md` |
| FR-09 | Should | A tournament participant can open one page showing the current draw, schedule and recorded results. | F7, F8; `interview-findings-requirements.md` |
| FR-10 | Should | After the next round is published, the participant receives a notification containing the assigned opponent and time (when notifications are enabled). | F7, F8; `interview-findings-requirements.md` |
| FR-11 | Should | Match history shows, for each recorded match, opponent(s), score and date. | F8; `interview-findings-requirements.md` |
| FR-12 | Must | The onboarding flow requests only the defined essential details and permits all optional profile fields to remain empty. | F12, F13; `interview-findings-requirements.md` |
| FR-13 | Could | An organizer can create level-based divisions; a participant is assigned only to an eligible division. | F14; `interview-findings-requirements.md` |
| FR-14 | Could | Where court availability is integrated, the system displays available slots for the chosen court and time. | F10, F11; `interview-findings-requirements.md` |
| FR-15 | Could | For a tournament allowing direct entry, an eligible player can complete registration in one submission. | C1; `interview-findings-requirements.md` |

**Evidence caveat:** Fxx and Cx refer to interview findings and contradictions, not to automated verification results. The original evidence-strength assessment remains in the interview findings document. FR-12 is an interview-derived preference rather than a verified consensus; its priority is retained as recorded.

## B. Additional functional requirements (FR-16–FR-33)

| ID | Priority | Acceptance criterion (observable outcome) | Traceability |
|---|---|---|---|
| FR-16 | Must | A registered user signs in with valid credentials; invalid credentials do not start an authenticated session. | UC-02 |
| FR-17 | Must | After sign-out, an attempt to perform an authenticated action requires signing in again. | UC-02 |
| FR-18 | Must | Valid profile edits persist and appear on the user's profile; another user cannot edit that profile. | UC-03 |
| FR-19 | Must | A player can create a tournament; only authorized organizers can manage that tournament. | UC-16, UC-17 |
| FR-20 | Must | A tournament with valid required details is saved and becomes visible in the tournament list when published. | UC-16 |
| FR-21 | Must | Authorized changes are reflected in the participant list; new registrations are refused when registration is closed. | UC-17 |
| FR-22 | Must | An eligible registration is recorded; the system rejects an ineligible or duplicate entry for the same tournament. | UC-07 |
| FR-23 | Must | A pending invitation is not treated as a confirmed team; acceptance confirms the team and rejection leaves it unconfirmed. | UC-08; Project Proposal |
| FR-24 | Must | Each paired player appears on at most one team; already confirmed premade teams are not modified; any unpaired remainder is identified. | UC-18, UC-14; F9 |
| FR-25 | Must | For a supported format, the generated draw contains only eligible players/teams and obeys that format's progression rules. The first supported format is TBD. | UC-19; Project Proposal |
| FR-26 | Must | A saved schedule change is visible to relevant participants; a match cannot reference a non-existent tournament participant. | UC-20, UC-05; F8 |
| FR-27 | Must | A valid result is visible as pending; submission alone does not trigger a rating update. | UC-09; FR-03 |
| FR-28 | Must | Confirmation changes the result to confirmed; dispute changes it to disputed; an unrelated account cannot do either. | UC-10, UC-11; FR-03 |
| FR-29 | Must | An authorized organizer can record a resolution; the result and resolution status are visible to affected participants. The rule for rating disputed results remains TBD. | UC-21 |
| FR-30 | Must | Repeating confirmation of the same match produces no additional rating change. | UC-15; FR-02, FR-03 |
| FR-31 | Must | After the organizer finalizes a tournament, players can view its final standings. | UC-22; F8 |
| FR-32 | Must | A registered user can view available tournaments and their dates, participation format, and registration status. | UC-04, UC-05 |
| FR-33 | Must | A new player's starting estimate is identifiable as self-assessed; later match-based ratings are presented as calculated values. | UC-03, UC-12; FR-01, FR-02; F2, F4 |

**Scope caveat:** Organizer workflows in FR-19–FR-31 largely originate from the agreed project proposal and use case diagram. There were no organizer interviews in the three-user sample; these rows are not presented as direct interview findings.

## C. Non-functional requirements (NFR-01–NFR-18)

| ID | Priority | Acceptance criterion (test or inspection) | Quality area |
|---|---|---|---|
| NFR-01 | Must | At least 95% of successful requests complete within 1.5 seconds, measured at the API boundary with 30 concurrent simulated users over a 10-minute test. | Performance |
| NFR-02 | Must | At least 95% of these operations complete within 3 seconds for 30 concurrent simulated users over a 10-minute test; unsuccessful operations are reported separately. | Performance |
| NFR-03 | Should | During usability testing, an in-progress indicator or relevant feedback becomes visible within 1 second of initiating a network request, including when the server is deliberately delayed. | Performance |
| NFR-04 | Must | Authorization tests confirm that unauthenticated requests are rejected and that players cannot edit other players' profiles, manage tournaments they do not organize, or confirm results on behalf of unrelated participants. | Security |
| NFR-05 | Must | Tests and configuration review confirm HTTPS for application-to-server communication, no plaintext passwords in persistent storage or logs, and no secrets committed to the repository. | Security |
| NFR-06 | Must | Negative tests confirm validation of malformed inputs, rejection of unauthorized state changes, and prevention of duplicate rating updates from replayed result-confirmation requests. | Security |
| NFR-07 | Must | Form inspection confirms that optional fields can be left blank and that each required field has a documented purpose. | Privacy |
| NFR-08 | Must | Access-control and interface tests confirm that ordinary users cannot retrieve another user's private contact details or precise location without an explicitly enabled sharing rule. | Privacy |
| NFR-09 | Should | A privacy notice is accessible during registration and from account settings, and explains collected data, intended uses and a contact or process for privacy requests. | Privacy |
| NFR-10 | Must | In a moderated test with at least five participants, at least four complete registration and initial skill self-assessment without assistance; problems are recorded. | Usability |
| NFR-11 | Must | In a moderated test with at least five participants, at least four complete each assigned task unaided; task completion time and mistakes are recorded. | Usability |
| NFR-12 | Should | Manual tests on at least one Android and one iOS device or simulator confirm readable content, non-overlapping controls, visible errors, and that text scaling to 200% does not block completion of the core tasks. | Usability |
| NFR-13 | Must | Automated integration tests show that a failed operation does not leave a partially applied rating update, and repeated confirmation requests do not cause additional rating changes. | Reliability |
| NFR-14 | Must | With network failure simulated during registration and result submission, the app displays an error or retry option; the backend state is verified before any success message is shown. | Reliability |
| NFR-15 | Should | A documented restore rehearsal recreates users, tournaments, matches and confirmed ratings from a test backup, with key records checked for consistency. | Reliability |
| NFR-16 | Must | Repository documentation provides repeatable setup, configuration and test instructions; both developers independently follow the applicable instructions on a clean development environment. | Maintainability / capacity |
| NFR-17 | Must | The repository contains automated tests for each of these areas, and the tests are executed and recorded before a release candidate is submitted. | Maintainability / capacity |
| NFR-18 | Should | A 10-minute test with 30 concurrently active simulated users exercising browsing, registration and result workflows completes with at least 99% successful requests, excluding intentionally invalid requests. | Maintainability / capacity |

**Measurement note:** The numeric NFR targets (30 concurrent users, response-time thresholds, and usability-test sample size) are **proposed**, not measured facts or formal service-level commitments. The evaluation report must record environment, dataset, test procedure and actual results. Never mark a criterion as passed without test evidence.

## D. Traceability from user evidence to requirements

| Finding / concern | Supported requirement IDs | Evidence status |
|---|---|---|
| F1, F5: unknown ability / visible rating | FR-01, FR-05 | Verified (3/3 for F1 and F5) |
| F2–F4: unreliable self-rating and initial assessment | FR-02, FR-33 | Mixed: F2–F4 verified; design mechanism requires validation |
| F6: need for suitable opponents or partners | FR-05, FR-06, FR-07 | F6 verified; availability/distance details from individual accounts |
| F7–F8: tournament draw, schedule and results | FR-09, FR-10, FR-11, FR-26, FR-31 | F8 verified; F7 single-source |
| F9: doubles partners selected informally | FR-08, FR-24 | Verified (2/2 asked); automation is a design response |
| F10–F11: availability and area | FR-06, FR-07, FR-14 | Single-source (P2); court integration unverified |
| F12: quick onboarding | FR-12, NFR-10 | Single-source (P2) |
| F14: suitable tournament divisions | FR-13 | Partially verified |
| F15: ratings after inactivity | FR-04 | Single-source (P1) |
| C1: ease of registration disputed | FR-15 | Contradictory feedback; Could priority retained |

## E. Unresolved consistency and verification issues

1. **Registration and contact details:** FR-12 says basic sign-up requires name, area and self-estimated level, whereas UC-01 describes email/password account creation. The team must distinguish account credentials from onboarding/profile fields and decide which fields are required; neither source has been edited here.
2. **Notifications:** FR-10 is Should, and the context diagram treats push notifications as planned. It is not a Must condition for initial acceptance.
3. **Courts:** FR-14 remains Could and cannot be treated as promised court booking; booking and payments remain out of initial scope.
4. **Tournament structure:** FR-25 requires one supported initial format, but the precise format remains TBD. A Swiss-style note in the use-case document is not a binding choice.
5. **Rating engine:** Elo/Glicko-2 selection, uncertainty handling, doubles updates and public level mapping remain subject to evaluation. Do not treat a recommendation in the technology comparison as an approved final specification.
6. **Result disputes:** FR-29 allows organizer resolution, but FR-03 requires opponent confirmation before rating impact. Whether resolved disputes can be counted is undecided; acceptance tests for rating effects must be refined after policy approval.
7. **Priority review:** Several organizer requirements are Must despite having no organizer interview evidence; they follow the project scope and must be validated with organizers or supervisor. The Should priority of FR-09 is preserved even though the first-release scope includes tournament presentation; the team should explicitly review that inconsistency before development.

## Completion and evidence procedure

For each **Must** requirement, record the linked test-case ID, test type (functional, integration, security, usability, or performance), date, environment and outcome (**Pass / Fail / Not tested**). The acceptance check above defines the expected result, not evidence that the feature has passed. Keep any future changes to the baseline in the original requirement file and mirror the priority/check here only after an agreed review.
