# Interview Findings → Requirements

**Project:** Amateur Tennis Community app
**Source:** `tennis-interviews.md` (3 user interviews)
**Purpose:** Turn interview findings into requirements and design decisions, showing what each one is based on.

## Participants

| ID | Profile | How they play | Tournaments |
|---|---|---|---|
| P1 | Amateur player, member of Astana Tennis Club community (~400 players) | Regularly, Sunday tournaments | Plays, has not organized |
| P2 | Student, casual player | Occasionally, with friends | Never played or organized |
| P3 | Player who trained with a coach | With a coach | Has played amateur tournaments (King of the Court) |

## Evidence levels

- **Verified:** said directly by at least 2 participants.
- **Single-source:** said directly by 1 participant. It's real evidence but nobody else confirmed it.
- **Assumption:** the team's inference or hypothesis. No participant said it, or it hasn't been tested.

Quotes are English translations. Timestamps (e.g. `P1 @0:45`) point to the transcripts. P3 references use the question number (e.g. `P3 Q2`).

---

## 1. Summary of recurring findings

1. **Not knowing an opponent's level is the main barrier** to finding people to play with (all 3).
2. **There is no reliable, shared rating.** Existing ones are local, outdated or missing, and people misreport their own level (all 3).
3. **Level is judged informally:** by watching, playing once, or asking a coach or organizer (all 3).
4. **Everyone wants a visible rating and a way to find a suitable partner or opponent.** These were the top needs named for the app (all 3).
5. **Players want tournament results, brackets and their next opponent visible in one place** (P1, P3).
6. **Doubles partners are picked from people players already know**, by observed skill (P1, P3).

---

## 2. Findings

| ID | Finding | Evidence | Status | → Linked to |
|---|---|---|---|---|
| F1 | Unknown skill level is the main barrier to choosing opponents | P1 @0:45 "first time you see someone and don't know their rating, it's hard to decide whether to play" · P2 @1:05 "not much fun playing someone much stronger or weaker" · P3 Q2 "hard… because of a possible skill gap" | Verified (3/3) | FR-01, FR-05 |
| F2 | Self-reported levels can't be trusted | P1 @3:31 "some people understate their rating… to find good partners" · P3 Q2 "some say they're bad and they're actually good… some brag" | Verified (2/3) | FR-02, FR-03, DD-02 |
| F3 | No shared, up-to-date rating exists | P1 @1:59 "the system is very old, almost never updated" · P2 @1:48 "no official rating… my judgment is purely subjective" · P3 Q4 "there was a level system, but I didn't have a rating" | Verified (3/3) | FR-02, FR-04 |
| F4 | Level is judged informally: watching, playing, or asking a coach or organizer | P1 @1:16 organizers' ratings plus own judgment · P2 @1:48 "shots, power, accuracy, movement… after one match you can tell" · P3 Q3 "from my coach" | Verified (3/3) | FR-02, DD-03 |
| F5 | Users want a visible rating that updates automatically | P1 @6:36 "just tracking people's ratings" (named as top need) · P2 @2:55 "a rating would be useful, especially with people I don't know" · P3 Q8 "have an Elo system" | Verified (3/3) | FR-01, FR-02 |
| F6 | Finding a suitable partner or opponent is the main reason to use the app | P2 @6:53 "finding a suitable opponent without extra effort" · P3 Q9 "partner or opponent search… matters most" · P1 @6:36 ratings "would help find partners quickly" (indirect) | Verified (3/3) | FR-05, FR-06, FR-07 |
| F7 | Tournament scores and next opponents get lost in WhatsApp/Telegram chats | P1 @2:45 "after every match you have to go back to the organizers and ask" · P1 @3:31 "hard to find in the chats who played whom" | Single-source (P1), partly contradicted by P3 (see C2) | FR-09, FR-10, DD-04 |
| F8 | Players want to see results, brackets and upcoming opponents | P1 @5:20 "see what score they finished with and who I might play next" · P3 Q8 "put people into brackets" | Verified (2/3) | FR-09, FR-10, FR-11 |
| F9 | Doubles partners are chosen from familiar players, by observed skill | P1 @4:38 "people I usually play with… pick a partner by eye" · P3 Q7 "people I've already played with" · P3 Q6 forming doubles teams is "the most inconvenient thing" | Verified (2/2 asked; P2 was not asked) | FR-08 |
| F10 | Availability and spontaneous play matter | P2 @1:05 "I might want to play on the weekend, but my friends have plans" · P2 @5:37 "suddenly want to play, find people, find a court, and go" | Single-source (P2) | FR-06, FR-14 |
| F11 | Distance to players and courts matters | P2 @5:37 "find players nearby" · P2 @6:53 "how far we'd have to go to a court" | Single-source (P2) | FR-07 |
| F12 | Onboarding must take little effort | P2 @6:53 "wouldn't want to spend a lot of time filling out a profile or figuring out a complicated player system" | Single-source (P2) | FR-12, DD-02 |
| F13 | Too few local users would make the app useless | P2 @6:53 "not much use if there's nobody nearby to play with" · P1 @0:12 an existing community of ~400 players already exists | Single-source (P2), but a critical risk | DD-01, FR-12 |
| F14 | Amateur tournaments should match players' level | P2 @4:34 "aimed at people of my level… not only experienced old-timers" · P3 Q4 "you usually don't get to play in very big tournaments if you're an amateur" | Verified (2/3), partial | FR-13 |
| F15 | Ratings become inaccurate when a player is inactive | P1 @1:59 "if someone is away for six months, their rating can drop and nobody keeps track of it" | Single-source (P1) | FR-04 |

---

## 3. Contradictory and uncommon feedback

### Contradictions

| ID | Topic | What was said | How we handle it |
|---|---|---|---|
| C1 | Is registration hard? | P2 @4:34 expects registration to be the hardest part, but **has never registered** (hypothetical). P3 Q5 has played tournaments and says "registration was easy." | We don't treat registration as a verified pain point. Keep it simple, but low priority (FR-15). |
| C2 | Is scheduling hard? | P1 @2:45 says chasing organizers and chats is painful. P2 @4:34 (hypothetical) worries about waiting hours and clashes with classes. P3 Q5 says "scheduling wasn't really hard." | The difference may come from who organizes: P3's coach and venue ran the event, while P1's community uses chats. Tournament features focus on **community-run** tournaments. Validate with organizers (see §6). |
| C3 | Which way do people misreport their level? | P1 @3:31 says people mostly **understate** it. P3 Q2 says **both ways**. | Either way, self-reports aren't reliable, so the rating is driven by results (FR-02). |
| C4 | How important is a rating? | For P1 it's the **top need**. P2 says his own judgment is enough with friends, but a rating helps with strangers. P3 puts **search above rating**. | For most users the rating is a means to matchmaking, not a feature on its own, so it's built into search (FR-05). |
| C5 | How complex should the rating be? | P3 Q8 asks for an Elo system. P2 @6:53 doesn't want "a complicated player system." | Elo-style calculation under the hood, with a simple level band in the UI (DD-02). |

### Uncommon feedback (one participant only, kept on record)

| ID | Feedback | Source | Effect |
|---|---|---|---|
| U1 | The coach is the trusted authority on a player's level | P3 Q3 | Optional coach or organizer confirmation of starting level (DD-03) |
| U2 | Apps exist for basketball and football in P2's country, but not for tennis | P2 @5:37 | A market-gap claim only. Needs desk research (A7). |
| U3 | Amateurs rarely get access to big tournaments | P3 Q4 | Supports level-based divisions (FR-13) |
| U4 | Ratings become inaccurate after a long absence | P1 @1:59 | Provisional or recency marker on ratings (FR-04) |

---

## 4. Assumptions (not verified by interviews)

| ID | Assumption | Why it matters | Affects |
|---|---|---|---|
| A1 | Players will trust a calculated rating more than self-reports | The rating approach depends on it | FR-02, DD-02 |
| A2 | Players will log results honestly, and opponents will confirm them | Without this the rating can be gamed | FR-02, FR-03 |
| A3 | Organizers or coaches will move tournaments from WhatsApp/Telegram into the app | **No organizers were interviewed** | FR-09, FR-10, DD-04 |
| A4 | Existing communities (e.g. the ~400-player club P1 mentioned) can provide the first users | Critical-mass risk (F13) | DD-01 |
| A5 | Users are willing to share an approximate location | Not asked | FR-07 |
| A6 | Court availability data can be obtained from venues | Not researched | FR-14 |
| A7 | There's no comparable tennis app in the target market | Based only on P2's claim | Overall scope |
| A8 | Users are willing to pay, and in what model | Not discussed | Business model |

---

## 5. Requirements and design decisions

Priority uses MoSCoW: **M**ust, **S**hould, **C**ould.

### Functional requirements

| ID | Requirement | Priority | Based on | Evidence strength |
|---|---|---|---|---|
| FR-01 | Every player profile shows their level as a simple band plus a numeric rating | M | F1, F5 | Verified |
| FR-02 | The rating updates automatically from confirmed match results (Elo-style). A self-assessed level or a coach's input only sets the starting value. | M | F2, F3, F4, F5 | Verified (algorithm: A1) |
| FR-03 | A match result counts only after the opponent confirms it | M | F2 | Verified need, mechanism is A2 |
| FR-04 | Ratings of new or inactive players are marked "provisional," with the date of the last match shown | S | F3, F15 | Single-source (P1) |
| FR-05 | Players can search for opponents and partners filtered by level range | M | F1, F6 | Verified |
| FR-06 | Search can filter by availability, including "play now / this weekend" posts | S | F6, F10 | Single-source (P2) |
| FR-07 | Search can filter by area or distance | S | F6, F11 | Single-source (P2), relies on A5 |
| FR-08 | Doubles: show partners the player has "played with before" and suggest level-balanced pairs | S | F9 | Verified (2/2 asked) |
| FR-09 | Each tournament has a page with bracket, schedule and results, visible to all participants | S | F7, F8 | Verified (F8), relies on A3 |
| FR-10 | Players get a notification with their next opponent and match time after each round | S | F7, F8 | Single-source (F7), relies on A3 |
| FR-11 | Each player has a match history: opponents, scores, dates | S | F8 | Verified |
| FR-12 | Minimal sign-up: name, area and self-estimated level. Everything else is optional. | M | F12, F13 | Single-source, low cost |
| FR-13 | Tournaments can be split into divisions by level band | C | F14 | Verified (2/3), partial |
| FR-14 | Players can find courts with free slots | C | F10, F11 | Single-source, relies on A6 |
| FR-15 | Tournament registration takes one step | C | C1 | Contradicted, low priority |

### Design decisions

| ID | Decision | Based on | Evidence strength |
|---|---|---|---|
| DD-01 | Launch through existing clubs and communities, area by area, rather than an open public launch, so each area has enough active players | F13 | Single-source risk, relies on A4 |
| DD-02 | Calculate ratings Elo-style but show users a simple level band (e.g. Beginner / Intermediate / Advanced with a number) | F2, F5, F12, C5 | Verified need, UI choice is A1 |
| DD-03 | Coaches or organizers can set or confirm a player's starting level | F4, U1 | Single-source |
| DD-04 | Move scores, brackets and next-match info out of chat messages into structured data, but let tournaments be shared as links into WhatsApp/Telegram instead of replacing those chats on day one | F7, C2 | Single-source, relies on A3 |

---

## 6. Limitations and next steps

**Limitations**
- Small sample (n = 3), all amateur players. The results show direction but are not representative.
- **No organizers or coaches were interviewed**, so organizer-side needs (FR-09, FR-10, DD-04) are unverified.
- P2 has never played a tournament, so his tournament feedback is anticipated, not experienced.
- The doubles question was skipped with P2. P3 gave no concrete example for Q2 and no concerns for Q9.
- Interviews 1–2 were transcribed automatically and translated from Russian. A few uncertain words are marked [?] in the transcripts.

**Next steps**
1. Interview 2–3 tournament organizers or coaches to check A3, C2, FR-09 and FR-10.
2. Test the rating concept (A1, A2) with a mock-up: would players trust it and confirm results?
3. Ask future participants about location sharing (A5) and willingness to pay (A8).
4. Desk research on existing tennis matchmaking apps in the target market (A7).
