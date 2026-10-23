# Requirements Priorities and Acceptance Criteria

**Project:** Amateur Tennis Community Platform  
**Task:** ATC-12 - Define Requirement Priorities and Acceptance Criteria  
**Status:** Draft v0.2 for team and supervisor review — updated after the consistency review of 23 October 2026  
**Coverage:** FR-01–FR-44 and NFR-01–NFR-22

## Purpose and source of truth

This matrix consolidates **existing** requirement IDs, priorities, and verifiable acceptance checks without renumbering or rewriting the requirements maintained in the source documents:

- `interview-findings-requirements.md`: FR-01–FR-15 (Arlan; priority and interview evidence preserved, with clarifications of FR-01, FR-03, FR-10 and FR-12).
- `functional-requirements-addition.md`: FR-16–FR-44 (additional functional requirements; the file was previously named `functional-requirements-addendum.md`).
- `non-functional-requirements.md`: NFR-01–NFR-22 (proposed quality thresholds and checks).
- `Usecase Diagram.md`: UC identifiers; `project-proposal.md`: scope baseline.

The wording of the authoritative requirement is maintained in its source file; the rows below describe **how compliance will be verified**. Reviewers should use the ID to locate the full requirement. No requirement is marked implemented or tested merely because its acceptance check has been defined.

These requirement documents are the reference for priorities. Other project documents (proposal, risk register, milestones, diagrams) follow them; where they disagreed, they were aligned in the consistency review.

## Priority scheme

- **Must (M):** required by the current documented baseline for the proposed first release.
- **Should (S):** desirable for a usable release, but may be deferred if capacity is limited.
- **Could (C):** optional extension, not required for acceptance of the initial release.

Priorities are copied from the source documents. Any change must be approved by the team and is recorded in the revision history at the end of this document; this matrix never silently upgrades a Should or Could to Must. Each requirement, including optional ones, has an acceptance check for possible later verification.

## A. Interview-derived functional requirements (FR-01–FR-15)

| ID | Priority | Acceptance criterion (observable outcome) | Evidence / source |
|---|---|---|---|
| FR-01 | Must | A player profile displays the NTRP-style level number with its labelled band (for example 3.5, Intermediate) and provisional status; the internal Glicko-2 value is not shown on player screens. | F1, F5; `interview-findings-requirements.md` |
| FR-02 | Must | After a confirmed match, the player rating changes according to the selected documented method; changing an initial self-assessment alone does not count as a confirmed match result. | F2, F3, F4, F5; `interview-findings-requirements.md` |
| FR-03 | Must | A submitted result remains pending and does not affect the rating until an eligible opponent confirms it, or until the organizer resolves a dispute about it (FR-29). | F2; `interview-findings-requirements.md` |
| FR-04 | Should | New or inactive players display a provisional indicator and the date of their last recorded match. | F3, F15; `interview-findings-requirements.md` |
| FR-05 | Must | A search with a chosen level range returns only players within that range (or a clearly labelled empty state). | F1, F6; `interview-findings-requirements.md` |
| FR-06 | Should | An availability filter restricts results to the selected time window; a published play-now/weekend request can be found. | F6, F10; `interview-findings-requirements.md` |
| FR-07 | Should | Selecting an area or distance filter restricts visible results accordingly when a player has opted to share the necessary location; distances are shown in bands (NFR-22). | F6, F11; `interview-findings-requirements.md` |
| FR-08 | Should | A player can view previous doubles partners and receive a proposed pairing generated from recorded levels. | F9; `interview-findings-requirements.md` |
| FR-09 | Should | A tournament participant can open one page showing the current draw, schedule and recorded results. | F7, F8; `interview-findings-requirements.md` |
| FR-10 | Should | After the next round is published, the participant sees the assigned opponent and time in the app (next-match card or in-app notification). Push delivery is optional and not required for this check. | F7, F8; `interview-findings-requirements.md` |
| FR-11 | Should | Match history shows, for each recorded match, opponent(s), score and date. | F8; `interview-findings-requirements.md` |
| FR-12 | Must | The onboarding flow requests only the defined essential details (name, area, self-estimated level, plus the credentials and consent in FR-34) and permits all optional profile fields to remain empty. | F12, F13; `interview-findings-requirements.md` |
| FR-13 | Could | An organizer can create level-based divisions; a participant is assigned only to an eligible division. | F14; `interview-findings-requirements.md` |
| FR-14 | Could | Where court availability is integrated, the system displays available slots for the chosen court and time. | F10, F11; `interview-findings-requirements.md` |
| FR-15 | Could | For a tournament allowing direct entry, an eligible player can complete registration in one submission. | C1; `interview-findings-requirements.md` |

**Evidence caveat:** Fxx and Cx refer to interview findings and contradictions, not to automated verification results. The original evidence-strength assessment remains in the interview findings document. FR-12 is an interview-derived preference rather than a verified consensus; its priority is retained as recorded.

## B. Additional functional requirements (FR-16–FR-44)

| ID | Priority | Acceptance criterion (observable outcome) | Traceability |
|---|---|---|---|
| FR-16 | Must | A registered user signs in with valid credentials; invalid credentials do not start an authenticated session. | UC-02 |
| FR-17 | Must | After sign-out, an attempt to perform an authenticated action requires signing in again, including when a token issued before sign-out is replayed. | UC-02; NFR-19 |
| FR-18 | Must | Valid profile edits persist and appear on the user's profile; another user cannot edit that profile. | UC-03 |
| FR-19 | Must | A player can create a tournament; only authorized organizers can manage that tournament. | UC-16, UC-17 |
| FR-20 | Must | A tournament with valid required details is saved and becomes visible in the tournament list when published. | UC-16 |
| FR-21 | Must | Authorized changes are reflected in the participant list; new registrations are refused when registration is closed. | UC-17 |
| FR-22 | Must | An eligible registration is recorded; the system rejects an ineligible or duplicate entry for the same tournament. | UC-07 |
| FR-23 | Must | A pending invitation is not treated as a confirmed team; acceptance confirms the team and rejection leaves it unconfirmed. | UC-08; Project Proposal |
| FR-24 | Must | Each paired player appears on at most one team; already confirmed premade teams are not modified; any unpaired remainder is identified. | UC-18, UC-14; F9 |
| FR-25 | Must | For Swiss-style test tournaments of 7, 8, 9 and 12 participants, every round contains only eligible participants, each participant appears at most once per round, no pairing repeats, and each bye goes to the lowest-ranked participant without a previous bye. | UC-19, UC-14; Project Proposal |
| FR-26 | Must | A saved schedule change is visible to relevant participants; a match cannot reference a non-existent tournament participant. | UC-20, UC-05; F8 |
| FR-27 | Must | A valid tournament-match result is visible as pending; submission alone does not trigger a rating update. | UC-09; FR-03 |
| FR-28 | Must | Confirmation changes the result to confirmed; dispute changes it to disputed; an unrelated account, the organizer acting for someone else, or the submitter's own doubles partner cannot do either. | UC-10, UC-11; FR-03 |
| FR-29 | Must | An authorized organizer can record a resolution (corrected score or void); the result and resolution status are visible to affected participants; a resolved score changes ratings exactly once and a void match changes none. | UC-21, UC-15 |
| FR-30 | Must | Repeating confirmation of the same match produces no additional rating change. | UC-15; FR-02, FR-03 |
| FR-31 | Must | After the organizer finalizes a tournament, players can view its final standings. | UC-22; F8 |
| FR-32 | Must | A registered user can view available tournaments and their dates, participation format, and registration status. | UC-04, UC-05 |
| FR-33 | Must | A new player's starting estimate is identifiable as self-assessed; later match-based ratings are presented as calculated values. | UC-03, UC-12; FR-01, FR-02; F2, F4 |
| FR-34 | Must | An account is created for a valid, unused email and a password that meets the password policy; a duplicate email is rejected; registration cannot finish without accepting the privacy notice; the password is stored only as a hash. | UC-01; FR-12; NFR-05, NFR-09, NFR-21 |
| FR-35 | Should | A password-reset link works once and expires after 30 minutes; after a reset, existing sessions are revoked. | UC-02; NFR-19 |
| FR-36 | Should | An account with an unverified email cannot publish a tournament; after the verification link is followed, it can. | UC-01, UC-16; Risk 14 |
| FR-37 | Must | After account deletion, the user cannot sign in, their profile is no longer visible, and other players' match histories show "Deleted player" with their ratings unchanged. | UC-03; NFR-07; Risk 8 |
| FR-38 | Should | A withdrawn participant is not paired in later Swiss rounds; their unplayed matches are recorded as walkovers that do not affect ratings. | UC-07, UC-17; Risk 3 |
| FR-39 | Should | An edited or cancelled tournament shows the updated details or a "Cancelled" status to all registered participants; a cancelled tournament accepts no further registrations or results. | UC-16, UC-17 |
| FR-40 | Should | A player's statistics match their confirmed results; the level history shows one entry for each rating change. | UC-13; F8 |
| FR-41 | Must | The organizer's attempts to submit or confirm another participant's result are rejected; for a disputed match in which the organizer played, "void" is the only available resolution and no rating changes. | UC-21; FR-29; Risk 14 |
| FR-42 | Must | After a result is submitted, disputed and resolved, its history shows all three steps with actor and time; each rating change is linked to the match that caused it. | UC-10, UC-15, UC-21; Risk 14 |
| FR-43 | Could | A casual match can be submitted and confirmed; until rating for casual matches is enabled, it appears in match history but does not change ratings. | UC-09; F6 |
| FR-44 | Could | Opening a shared tournament link shows the tournament page, after sign-in if needed. | UC-04; DD-04; F7 |

**Scope caveat:** Organizer workflows in FR-19–FR-31 and FR-36–FR-42 largely originate from the agreed project proposal, the use case diagram and the risk register. There were no organizer interviews in the three-user sample; these rows are not presented as direct interview findings.

## C. Non-functional requirements (NFR-01–NFR-22)

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
| NFR-09 | Must | A privacy notice is accessible during registration and from account settings, and explains collected data, intended uses, storage location and a contact or process for privacy requests, including account deletion; registration cannot be completed without accepting it. | Privacy |
| NFR-10 | Must | In a moderated test with at least five participants, at least four complete registration and initial skill self-assessment without assistance; problems are recorded. | Usability |
| NFR-11 | Must | In a moderated test with at least five participants, at least four complete each assigned task unaided; task completion time and mistakes are recorded. | Usability |
| NFR-12 | Should | Manual tests on at least one Android and one iOS device or simulator confirm readable content, non-overlapping controls, visible errors, and that text scaling to 200% does not block completion of the core tasks. | Usability |
| NFR-13 | Must | Automated integration tests show that a failed operation does not leave a partially applied rating update, and repeated confirmation requests do not cause additional rating changes. | Reliability |
| NFR-14 | Must | With network failure simulated during registration and result submission, the app displays an error or retry option; the backend state is verified before any success message is shown. | Reliability |
| NFR-15 | Should | A documented restore rehearsal recreates users, tournaments, matches and confirmed ratings from a test backup, with key records checked for consistency. | Reliability |
| NFR-16 | Must | Repository documentation provides repeatable setup, configuration and test instructions; both developers independently follow the applicable instructions on a clean development environment. | Maintainability / capacity |
| NFR-17 | Must | The repository contains automated tests for each of these areas, and the tests are executed and recorded before a release candidate is submitted. | Maintainability / capacity |
| NFR-18 | Should | A 10-minute test with 30 concurrently active simulated users exercising browsing, registration and result workflows completes with at least 99% successful requests, excluding intentionally invalid requests. | Maintainability / capacity |
| NFR-19 | Must | Access tokens are valid for at most 30 minutes and carry a session ID checked on every request; a token captured before sign-out or a password reset is rejected with 401 afterwards. | Security |
| NFR-20 | Must | On a test device, tokens are kept only in iOS Keychain / Android Keystore; no token or password appears in the Drift cache, plain key-value preferences or logs. | Security |
| NFR-21 | Must | After 5 failed sign-in attempts for one account within 15 minutes, further attempts are blocked for 15 minutes; passwords shorter than 8 characters are rejected; error messages do not reveal whether an email is registered. | Security |
| NFR-22 | Should | Search results show distance only in coarse bands and never coordinates; queries from several positions cannot narrow a player's location below the band size. | Privacy |

**Measurement note:** The numeric NFR targets (30 concurrent users, response-time thresholds, token lifetime, lockout thresholds and usability-test sample size) are **proposed**, not measured facts or formal service-level commitments. The evaluation report must record environment, dataset, test procedure and actual results. Never mark a criterion as passed without test evidence.

## D. Traceability from user evidence to requirements

| Finding / concern | Supported requirement IDs | Evidence status |
|---|---|---|
| F1, F5: unknown ability / visible rating | FR-01, FR-05 | Verified (3/3 for F1 and F5) |
| F2–F4: unreliable self-rating and initial assessment | FR-02, FR-33 | Mixed: F2–F4 verified; design mechanism requires validation |
| F6: need for suitable opponents or partners | FR-05, FR-06, FR-07 | F6 verified (2/3 direct, P1 indirect); availability/distance details from individual accounts |
| F7–F8: tournament draw, schedule and results | FR-09, FR-10, FR-11, FR-26, FR-31, FR-44 | F8 verified; F7 single-source |
| F9: doubles partners selected informally | FR-08, FR-24 | Verified (2/2 asked); automation is a design response |
| F10–F11: availability and area | FR-06, FR-07, FR-14, NFR-22 | Single-source (P2); court integration unverified |
| F12: quick onboarding | FR-12, FR-34, NFR-10 | Single-source (P2) |
| F14: suitable tournament divisions | FR-13 | Partially verified |
| F15: ratings after inactivity | FR-04 | Single-source (P1) |
| C1: ease of registration disputed | FR-15 | Contradictory feedback; Could priority retained |
| Risk 14: rating manipulation | FR-36, FR-41, FR-42 | Design response; no interview evidence |

## E. Consistency issues and their resolution

All items below were open in v0.1 and were resolved in the consistency review of 23 October 2026.

1. **Registration and contact details:** FR-12 lists the essential profile fields (name, area, self-estimated level); FR-34 adds the account credentials (email and password) and privacy-notice consent required by UC-01. The registration screen must ask for exactly these fields.
2. **Notifications:** FR-10 stays Should and is met in the app (next-match card and in-app notification list). Push delivery through FCM/APNs is Could, consistent with the risk register and the context and component diagrams, where push services are marked as planned.
3. **Courts:** FR-14 remains Could and cannot be treated as promised court booking; booking and payments remain out of initial scope.
4. **Tournament structure:** Swiss-style is the first supported format; FR-25 now states its rules. Other formats remain later extensions.
5. **Rating engine:** Glicko-2 is the selected method, with Elo implemented behind the same interface as a fallback and evaluation baseline. Rating-period handling, initial values, doubles aggregation and displayed-level mapping are still to be defined in milestone 4.
6. **Result disputes:** the opponent confirms or disputes (FR-03, FR-28); the organizer resolves disputes, and a resolved score counts once (FR-29); an organizer cannot resolve a dispute in a match they played (FR-41). Acceptance tests for rating effects follow FR-29 and FR-30.
7. **Priority review:** Organizer requirements remain Must on the basis of the project scope and must still be validated with organizers or the supervisor (milestone 2). FR-09 stays Should: the Must requirements FR-26 (schedule) and FR-31 (final standings) already require tournament information to be displayed; FR-09 adds the single combined page.

## Revision history

| Date | Change |
|---|---|
| 18 October 2026 | v0.1: matrix for FR-01–FR-33 and NFR-01–NFR-18. |
| 23 October 2026 | v0.2 (consistency review): Swiss-style selected as first format (FR-25); dispute rule decided (FR-29); FR-34–FR-44 and NFR-19–NFR-22 added; **NFR-09 raised from Should to Must** because the personal-data mitigation (Risk 8) depends on consent at sign-up; acceptance checks of FR-01, FR-03, FR-10, FR-12, FR-17, FR-27, FR-28 clarified; section E resolved. No other priority changed. |

## Completion and evidence procedure

For each **Must** requirement, record the linked test-case ID, test type (functional, integration, security, usability, or performance), date, environment and outcome (**Pass / Fail / Not tested**). The acceptance check above defines the expected result, not evidence that the feature has passed. Keep any future changes to the baseline in the original requirement file and mirror the priority/check here only after an agreed review.
