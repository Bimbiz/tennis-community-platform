# Comparison of Technology Alternatives

This document compares technology options for the key technical decisions in our diploma project, a cross-platform mobile app for amateur tennis players and organizers. The app handles tournament management, registration, opponent and partner matching, match results and automatic rating calculation.

We cover six decisions. Three of them (mobile framework, backend framework and architecture) were made before this comparison, and here we check that they hold up against the alternatives. For the other three (database, local storage and rating algorithm) this document compares the options, and the team selected the recommended option for each. Each decision compares three options on the same criteria.

## What the technology has to support

These needs come from the project scope and our requirements:

- **Cross-platform app.** One app for Android and iOS, used by both players and organizers.
- **Two developers working in parallel.** Timur builds the mobile app and Arlan builds the backend, so we need a clear API contract between them. We already plan to use REST with JSON and an OpenAPI description.
- **Server-side ratings.** Ratings are calculated on the server from confirmed match results. A result has to be submitted by one player and confirmed by the other before it counts, and nobody should be able to change a rating directly.
- **Connected data.** Tournaments, singles and doubles formats, individual and team registrations, automatically formed doubles pairs, schedules, matches, results, rating history and statistics are all linked to each other.
- **Two kinds of rating.** An internal rating, Elo or Glicko-2, and a simpler NTRP-style level shown to players. The rating should handle new players and players returning after a break, which came up in our interviews.
- **Limited time.** We have to deliver a working, testable system within the diploma timeline, which makes development speed and maintainability important.

## 1. Mobile framework

Options: Flutter (Dart), React Native (JavaScript/TypeScript), and separate native apps (Kotlin for Android, Swift for iOS).

| | Flutter | React Native | Native (Kotlin + Swift) |
|---|---|---|---|
| One codebase for Android and iOS | Yes | Yes | No, two separate apps |
| Development speed | Fast, with hot reload and a large set of built-in widgets | Fast, with fast refresh | Slow, every screen is built twice |
| UI consistency across platforms | Identical, because Flutter draws its own UI | Close, but uses each platform's native components | Each app follows its own platform |
| Support for local storage, HTTP and notifications | Mature packages, e.g. Drift for local data [2] | Mature packages | Full platform support |
| Fit with our team | Timur already works in Flutter/Dart | Would need to learn JavaScript/TypeScript and React | Would need to learn two languages |
| Main advantage | Fast development with a consistent UI | Large JavaScript ecosystem | Best performance and platform integration |
| Main drawback | Dart is used only on the mobile side | Less consistent UI, and a new stack for us | Double the work for a one-person mobile team |

**Decision: Flutter.** With one mobile developer, building two native apps isn't realistic. React Native would also work technically, but it offers us nothing Flutter doesn't, and Timur would have to switch stacks. Flutter gives us one codebase, a UI that looks the same on both platforms (useful for brackets and schedules), and good packages for everything in our scope.

## 2. Backend framework

Options: FastAPI (Python), Django REST Framework (Python), and NestJS (Node.js/TypeScript).

We also briefly considered a backend-as-a-service such as Firebase or Supabase. We ruled it out because rating calculation, partner formation and tournament scheduling are core logic that we want to write, test and control ourselves.

| | FastAPI | Django REST Framework | NestJS |
|---|---|---|---|
| OpenAPI contract for the mobile app | Generated automatically, with Swagger UI and ReDoc built in [1] | Usually through an extra package such as drf-spectacular | Supported through the separate @nestjs/swagger module |
| Request validation | Built in through Pydantic and Python type hints [1] | Through serializers, with more boilerplate | Through decorators and validation pipes |
| Authentication | OAuth2 and JWT support built in [1] | Session auth built in, JWT through extra packages | Through Passport and JWT modules |
| Rating maths and data processing | Python, with strong libraries for calculations | Python | Fewer numerical libraries |
| Learning curve and amount of code | Small and explicit | Larger framework with its own conventions (admin, ORM, apps) | Larger framework with heavy use of decorators |
| Fit with our team | Arlan already works with Python/FastAPI | Same language, but a different framework | Would need to switch languages |
| Main advantage | Fast to build, with a typed API and docs generated for free | Batteries included, including an admin panel | Structured, with TypeScript end to end |
| Main drawback | We choose and wire up the ORM and other parts ourselves | Heavier than we need for a pure API | New language for our backend developer |

**Decision: FastAPI.** The main reason is the API contract. FastAPI generates the OpenAPI description directly from our code [1], so the mobile side always has up-to-date documentation and can generate a Dart client from it. Validation through Pydantic models also cuts the risk of bad data reaching the rating logic. Django's admin panel is tempting for organizers, but organizers will use our mobile app, so it adds weight without much benefit.

## 3. Backend architecture

Options: a modular monolith, microservices, and a traditional layered monolith.

| | Modular monolith | Microservices | Layered monolith |
|---|---|---|---|
| Deployment | One application | Many services, each deployed separately | One application |
| Clear boundaries between features | Yes, each module (users, tournaments, matches, ratings, matchmaking) owns its own code | Yes, enforced by the network | Weak. Code is split by layer, so features get mixed together. |
| Transactions across features | Simple. Confirming a result and updating ratings happen in one database transaction. | Hard, and needs extra patterns for data spread across services | Simple |
| Effort for a two-person team | Low | High: networking, monitoring, several databases | Low |
| Path to growth | Modules can be split into services later if needed | Already split | Hard to split later |
| Main advantage | Simple to run, with clean structure | Independent scaling and deployment | Simplest to start |
| Main drawback | Module boundaries need discipline | Far too much overhead for our size | Gets tangled as features grow |

**Decision: modular monolith.** Confirming a match result and updating both players' ratings must happen together, and inside one application with one database that is a single transaction. Microservices would make this much harder and add infrastructure two people can't realistically maintain. Splitting the code into feature modules keeps the system organized, and a module could become its own service later if needed.

## 4. Database (selected: PostgreSQL)

Options: PostgreSQL, MySQL and MongoDB.

| | PostgreSQL | MySQL | MongoDB |
|---|---|---|---|
| Connected data (tournaments, matches, registrations, teams) | Natural fit, with tables, foreign keys and joins | Natural fit | Possible, but documents work best when data is nested inside each other |
| Transactions for result confirmation and rating updates | Full ACID transactions | Full ACID transactions | Supported for multiple documents, but less natural |
| Statistics and rating history | Strong SQL, including window functions | Good SQL | Aggregation pipelines |
| Room for future features | JSONB columns for flexible data, and the PostGIS extension if we add location-based search later | Fewer extensions | Built-in location queries |
| Support in the Python ecosystem | Very good (SQLAlchemy, async drivers) | Very good | Good, but outside the usual SQL tooling |
| Main advantage | Feature-rich, reliable and well suited to our data | Simple and widely hosted | Flexible schema |
| Main drawback | Slightly more setup than MySQL | Fewer advanced features | Harder to keep related data consistent |

**Decision: PostgreSQL.** Our data is clearly relational, and the most important operation, confirming a result and updating ratings, needs proper transactions. MySQL would also handle our current scope, so this was a closer call than MongoDB. PostgreSQL wins on extras that fit our plans: JSONB for things like tournament settings, and PostGIS if we add "players near me" search later.

## 5. Local storage on the device (selected: Drift, for the optional offline cache)

Options: Drift, sqflite and Hive.

Local storage lets the app show tournaments, schedules and match history without waiting for the network. It also means a player can view their next match at the courts even with a weak connection. That second point is our assumption: none of our interviewees mentioned connectivity problems, so the offline cache is a "could have" feature and is only built if time allows.

| | Drift | sqflite | Hive |
|---|---|---|---|
| Data model | SQLite with tables and relations | SQLite with tables and relations | Key-value boxes, no relations |
| Type safety | Generated, type-safe code. Mistakes are caught at compile time. [2] | Raw SQL strings and maps, so errors only show at runtime | Typed objects through adapters |
| Updating the UI when data changes | Any query can become an auto-updating stream [2] | Manual | Listenable boxes |
| Schema migrations and transactions | Built in [2] | Manual | Not applicable in the same way |
| Setup effort | Needs code generation | Minimal | Minimal |
| Main advantage | Safe, reactive and suited to relational data | Simple and lightweight | Very fast for simple data |
| Main drawback | Code generation adds a build step | A lot of manual work and no compile-time checks | Poor fit for related data such as tournaments, matches and players |

**Decision: Drift.** The data we cache is relational, and Drift's auto-updating queries fit well with Flutter screens that should refresh when new results arrive. The extra code-generation step is a small cost for type safety. Login tokens are never kept in Drift or in a plain key-value store: they go into the platform's secure storage (Keychain on iOS, Keystore on Android, for example through `flutter_secure_storage`), as NFR-20 requires. Simple user preferences can use a key-value store.

## 6. Rating algorithm (selected: Glicko-2)

Options: Elo, Glicko-2, and OpenSkill (a Weng-Lin model similar to Microsoft's TrueSkill).

| | Elo | Glicko-2 | OpenSkill |
|---|---|---|---|
| How it works | One number per player, adjusted after each match | Rating plus rating deviation (how certain the rating is) and volatility [3] | Bayesian skill estimate with an uncertainty value [4] |
| New players | Treated like everyone else, so early ratings are unreliable | High deviation at the start, so ratings move quickly until they settle [3] | High uncertainty at the start |
| Players returning after a break | No change | Deviation "will increase slowly over time of inactivity", so the rating is treated as less certain [3] | No built-in handling. Uncertainty would have to be raised by our own code. |
| Doubles | Usually by averaging the two partners' ratings | Same approach, e.g. treating a team as the average of its two players, as UTR does for doubles [5] | Built-in support for teams [4] |
| Easy to explain to players and at the defence | Very easy | Moderate | Harder, being a Bayesian model |
| Licensing and availability | Free to use | Public domain [3], with implementations in many languages | MIT-licensed Python library [4] |
| Main advantage | Simplest to build and explain | Handles uncertainty and inactivity, both of which matter for amateurs | Designed for teams |
| Main drawback | Can't tell a new player from an established one | Updates work in "rating periods", which need to be defined | Less common, and harder to justify and tune |

**Decision: Glicko-2.** Amateur players play irregularly, new players join all the time, and our interviews showed that ratings become unreliable when someone stops playing for a while. Glicko-2 handles exactly this through the rating deviation, which grows during inactivity [3][6]. We can use the same value to mark a player's displayed level as "provisional" while it is high. For doubles, we would treat a team as the average of its two players and update both partners, similar to how UTR handles doubles [5]. We would also keep separate singles and doubles ratings. OpenSkill's native team support is attractive, but it would be harder to explain and tune within our timeline. Plain Elo is implemented behind the same interface, as a fallback and as the baseline we compare Glicko-2 with in the evaluation.

**Rating period.** The architecture updates ratings in the same transaction as the result confirmation, so we plan to process each confirmed match as its own rating period and to increase a player's rating deviation according to the time since their last match. Glickman notes that the system works best when players have an average of at least 10–15 games per rating period [6], so we will test this choice with simulated seasons in milestone 4 before relying on it. If it gives unstable ratings, the alternative is a fixed period (for example one week or one tournament) with the displayed level updated at the end of each period.

One more detail still needs to be decided:

- **Mapping to displayed levels.** How internal ratings map to the NTRP-style levels players see.

## Summary

| Decision | Choice | Status |
|---|---|---|
| Mobile framework | Flutter (Dart) | Decided, confirmed by this comparison |
| Backend framework | FastAPI (Python) | Decided, confirmed by this comparison |
| Backend architecture | Modular monolith | Decided, confirmed by this comparison |
| Database | PostgreSQL | Selected |
| Local storage | Drift (SQLite) for the optional offline cache; secure storage for tokens | Selected |
| Rating algorithm | Glicko-2, with separate singles and doubles ratings; Elo as fallback and baseline | Selected |

Taken together, the stack gives us one mobile codebase and a typed API contract generated from the backend, so the two of us can work in parallel. Rating updates stay safe because they happen in a single database transaction inside one application, and the rating model handles new and returning players.

**Still to decide later:**
- Push notifications (a "could have" feature)
- State management in Flutter
- The ORM and migration tool on the backend
- Hosting

## Sources

1. FastAPI, *Features*: https://fastapi.tiangolo.com/features/
2. Drift documentation (pub.dev): https://pub.dev/documentation/drift/latest/
3. *Glicko rating system*, Wikipedia: https://en.wikipedia.org/wiki/Glicko_rating_system
4. OpenSkill on PyPI: https://pypi.org/project/openskill/
5. Universal Tennis Support, *FAQ: Doubles algorithm*: https://support.universaltennis.com/support/solutions/articles/9000183289-faq-doubles-algorithm
6. Mark E. Glickman, *Example of the Glicko-2 system*: http://www.glicko.net/glicko/glicko2.pdf
