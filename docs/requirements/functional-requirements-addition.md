# Functional Requirements Addition

**Project:** Amateur Tennis Community Platform  
**Task:** ATC-10 — Define Functional Requirements  
**Status:** Draft v0.1 
**Scope:** Additional requirements, FR-16–FR-33

## Purpose and numbering

This document **supplements**, rather than replaces, the fifteen functional requirements (FR-01–FR-15) in `interview-findings-requirements.md`. Those original IDs and their wording are preserved. The requirements below cover essential user and organizer workflows that were not stated explicitly in the interview-derived list. Together, the two documents form the current draft functional-requirements baseline.

**Priorities:** M = Must have for the agreed core workflow; S = Should have; C = Could have.  
**Traceability:** UC-XX refers to `Usecase Diagram.md`; FXX refers to findings in `interview-findings-requirements.md`. A dash means the item is primarily derived from the Project Proposal / system use cases rather than direct interview evidence.

## Additional functional requirements

| ID | Requirement | Priority | Source / use case | Acceptance check |
|---|---|---|---|---|
| **FR-16** | The system shall allow a person with valid account credentials to sign in and shall reject invalid credentials without granting access. | M | UC-02 | A registered user signs in with valid credentials; invalid credentials do not start an authenticated session. |
| **FR-17** | The system shall allow an authenticated user to sign out and prevent the signed-out session from accessing account-specific actions. | M | UC-02 | After sign-out, an attempt to perform an authenticated action requires signing in again. |
| **FR-18** | The system shall allow an authenticated user to view and edit their own basic profile information and save valid changes. | M | UC-03 | Valid profile edits persist and appear on the user's profile; another user cannot edit that profile. |
| **FR-19** | The system shall allow an authenticated user to act as a player and, when authorized for a tournament, as its organizer, without requiring a separate user account. | M | UC-16, UC-17 | A player can create a tournament; only authorized organizers can manage that tournament. |
| **FR-20** | The system shall allow a tournament organizer to create and publish a tournament with its name, dates, Singles/Doubles participation format, registration period, and applicable rules. | M | UC-16 | A tournament with valid required details is saved and becomes visible in the tournament list when published. |
| **FR-21** | The system shall allow a tournament organizer to view the participant list, accept or remove registrations, and close registration before play begins. | M | UC-17 | Authorized changes are reflected in the participant list; new registrations are refused when registration is closed. |
| **FR-22** | The system shall allow an eligible player to register for an open Singles tournament and to register individually for an open Doubles tournament, subject to tournament rules. | M | UC-07 | An eligible registration is recorded; the system rejects an ineligible or duplicate entry for the same tournament. |
| **FR-23** | For a Doubles tournament, the system shall allow a player to propose a premade team and shall register that team only after the invited partner accepts. | M | UC-08; Project Proposal | A pending invitation is not treated as a confirmed team; acceptance confirms the team and rejection leaves it unconfirmed. |
| **FR-24** | Before a Doubles tournament begins, an authorized organizer shall be able to request automatic formation of teams from eligible, unpaired registrants using the system's skill-based pairing rules. | M | UC-18, UC-14; F9 | Each paired player appears on at most one team; already confirmed premade teams are not modified; any unpaired remainder is identified. |
| **FR-25** | The system shall generate match pairings or a draw for a tournament according to an explicitly selected and supported competition format. | M | UC-19; Project Proposal | For a supported format, the generated draw contains only eligible players/teams and obeys that format's progression rules. The first supported format is TBD. |
| **FR-26** | The system shall allow an organizer to assign and update match times and court identifiers and shall display the current schedule to participants. | M | UC-20, UC-05; F8 | A saved schedule change is visible to relevant participants; a match cannot reference a non-existent tournament participant. |
| **FR-27** | The system shall allow an authorized participant to submit a score for a match they played and shall record it as pending until the confirmation process is completed. | M | UC-09; FR-03 | A valid result is visible as pending; submission alone does not trigger a rating update. |
| **FR-28** | The system shall allow the eligible opposing participant or representative of the opposing team to confirm a pending result or mark it as disputed. | M | UC-10, UC-11; FR-03 | Confirmation changes the result to confirmed; dispute changes it to disputed; an unrelated account cannot do either. |
| **FR-29** | The system shall allow the tournament organizer to inspect a disputed result and record a resolution decision with an auditable status. | M | UC-21 | An authorized organizer can record a resolution; the result and resolution status are visible to affected participants. The rule for rating disputed results remains TBD. |
| **FR-30** | A confirmed match result shall affect each participating player's rating no more than once, even if confirmation is repeated or the request is retried. | M | UC-15; FR-02, FR-03 | Repeating confirmation of the same match produces no additional rating change. |
| **FR-31** | The system shall retain a completed tournament's final standings and make them available to its participants. | M | UC-22; F8 | After the organizer finalizes a tournament, players can view its final standings. |
| **FR-32** | The system shall allow users to browse published tournaments and view the relevant tournament details before registering. | M | UC-04, UC-05 | A registered user can view available tournaments and their dates, participation format, and registration status. |
| **FR-33** | The system shall distinguish a user's initial self-assessed level from the rating calculated from confirmed match results. | M | UC-03, UC-12; FR-01, FR-02; F2, F4 | A new player's starting estimate is identifiable as self-assessed; later match-based ratings are presented as calculated values. |

## Existing requirements retained without renumbering

The original **FR-01–FR-15** already address rating display and updates, confirmation of results, provisional ratings, opponent/partner search, availability and distance filters, doubles suggestions, tournament information, notifications, match history, minimal onboarding, level divisions, court availability, and streamlined registration. These remain maintained in `interview-findings-requirements.md` and **are not duplicated or redefined here**.

## Open decisions and constraints

- **First tournament system:** TBD. The references to Swiss-style rounds in the use-case description are illustrative and are not a commitment that Swiss is the first implemented format.
- **Rating algorithm:** Elo and Glicko-2 are being evaluated; the technology comparison recommends Glicko-2, but this document specifies observable behavior rather than mandating an algorithm.
- **Disputed results:** The current FR-03 says results count after opponent confirmation. Whether an organizer-resolved result may enter the rating calculation requires a joint rule decision; FR-29 deliberately does not override FR-03.
- **Priorities:** Existing FR-01–FR-15 priorities remain exactly as recorded, even where they differ from the longer-term project scope. The new Must priorities describe the proposed initial end-to-end tournament workflow and require team confirmation.
- **User evidence:** Interviews support rating, matchmaking, and viewing tournament information, but no tournament organizers were interviewed. Organizer requirements therefore originate mainly from the project scope and use-case diagram and still require validation.
- **External services:** Push delivery and email verification/reset are not added as Must requirements, because their provision remains subject to scope decisions. Original FR-10 (notification) remains unchanged.

## Traceability note

A final cross-document traceability matrix can refer to FR-01–FR-15 in the interview findings and FR-16–FR-33 in this addition, without changing the original IDs. Use-case IDs UC-01 (registration), UC-06/UC-14 (opponent matching), and UC-12/UC-15 (rating) are largely covered by existing requirements; the additional requirements fill gaps in authentication, account/profile actions, organizer operations, tournament registration, team formation, scheduling, and disputed results.
