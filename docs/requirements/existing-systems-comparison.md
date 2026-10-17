# Comparison of Existing Tennis Systems

Before building our app, we looked at what already exists for amateur tennis players. We focused on the four things our app is meant to do: rate players by skill, help them find opponents and partners, support community interaction, and run tournaments.

We chose five systems: three international apps, the official ITF rating, and one local tournament league in Kazakhstan, because that is where our interview participants play. The information comes from the systems' official websites, help pages and press articles, all checked on 17 October 2026. We did not install or test the apps ourselves, so the comparison is based on what they publicly describe.

## The systems

**UTR Sports.** UTR (Universal Tennis Rating) is probably the best-known amateur rating. All players are rated on one scale from 1.00 to 16.50, calculated only from real match results [2]. The rating is a weighted average of a player's last 30 eligible matches from the past 12 months. Results from official events count towards a separate "Verified" rating, while self-reported matches only count towards the general one [2]. Doubles has its own rating [4]. The app helps players find local players, matches, leagues and events at their level [1][3]. A basic profile is free, and a paid "Power" subscription adds analytics, player scouting and discounts on event fees [3].

**Playtomic.** Playtomic is mainly a court booking app for padel and tennis clubs. New players answer a one-time questionnaire to get a starting level. After that, the level changes with every competitive match, based on the result, the opponents' levels and the partner's level [5]. Playtomic also tracks how reliable each level is, so a new player's level moves faster than an established one [5]. Clubs can publish "open matches" for others to join. The club sets the allowed level range, and players can turn down someone whose level doesn't fit. The court is booked once the match is full, and each player pays their share online [6].

**Global Tennis Network (GTN).** GTN is an online community for finding tennis partners. Members can search for players near them and get a level calculated from the matches they play [7][8]. It also supports ladders, leagues and tournaments, and has a forum and a directory of courts. Some features, such as private messaging, are only for paying members [7][8]. Reported membership is between 110,000 and 149,000 players, depending on the source [7][8].

**ITF World Tennis Number (WTN).** WTN is the International Tennis Federation's official rating, on a scale from 40 to 1 [9]. Players get it through their national federation, and several countries show separate singles and doubles numbers [10]. From August 2026, the UK version also takes game scores within each set into account and adjusts the ratings of players returning after a break [9]. Kazakhstan's tennis federation already shows WTN values in its ratings section [10]. WTN is only a rating, though. The sources describe player search and head-to-head comparisons, but no matchmaking, community or tournament features [10].

**Tennis League TS (TLTS).** TLTS organizes amateur tournaments in Kazakhstan. It was founded in November 2022 and had over 200 members by 2024 [11]. It runs a series of doubles tournaments where players collect points towards a season final, in categories such as Masters and Grand Masters [11]. The 2026 season had seven TS CUP rounds and a final on 25 September [12]. Players sign up through a form on the website [11]. The site shows a ratings table but doesn't explain how it is calculated, and there is no mobile app or partner search [12]. Its members are described mostly as businesspeople and managers [11].

## Comparison

All five systems are compared on the same eight criteria, with our planned app alongside for reference. "Not found" means we couldn't confirm the feature from public sources, not that it definitely doesn't exist.

| Criterion | UTR Sports | Playtomic | GTN | WTN | TLTS | Our app (planned) |
|---|---|---|---|---|---|---|
| Rating based on match results | Yes, 1.00–16.50 scale [2] | Yes, after a starting questionnaire [5] | Yes, method not published [8] | Yes, 40–1 scale [9] | Points table, method not published [11][12] | Yes |
| How trustworthy the rating is | Verified and self-reported results kept apart [2] | Reliability score for each player [5] | Not found | Confidence level in some countries, inactivity adjustment from 2026 [9][10] | Not found | Results confirmed by the opponent. New and inactive players marked as provisional. |
| Finding players by level | Yes [1] | Open matches with a level range [6] | Search nearby players by level [7] | No [10] | No [12] | Yes, by level, distance and availability |
| Doubles | Separate doubles rating [4] | Partner's level is counted [5] | Not found | Separate doubles number [10] | Doubles tournaments [11] | Past partners shown, balanced pairs suggested |
| Tournaments and leagues | Yes, run by registered event providers [1][3] | Not found | Ladders, leagues and tournaments [8] | No | Its own tournament series [11] | Brackets, results and notifications for any community organizer |
| Community and communication | Clubs, groups, meetups [1][3] | Not found | Forum, meetups, messaging for paying members [7][8] | No | Website only [12] | Links that can be shared into existing group chats |
| Used in Kazakhstan | Not found | Not found | Not found | Shown by the national federation [10] | Yes, based in Almaty [12] | Launch through local clubs |
| Cost for players | Free, with a paid tier [3] | Pay per court booking [6] | Free, with a paid tier [8] | Depends on the country [9][10] | Not published | Not decided yet |

## What the comparison shows

Calculating a player's level from match results is now the norm: four of the five systems do it. That supports our decision not to rely on players describing their own level. The more mature systems, UTR and Playtomic, also show how certain a rating is, which we plan to do as well.

UTR comes closest to what we are planning. It covers ratings, finding players, doubles and events. For our users, its weak points are that we found no sign of UTR events or communities in Kazakhstan, and that its tournament tools are aimed at registered event providers rather than someone running a weekend tournament for their club.

The local option, TLTS, is a tournament league rather than a way to find players, and its rating method isn't public. WTN is already used in Kazakhstan, but it is only a number. It may be more useful to us as an optional starting level for new players than as a competitor.

## Why our app is still worth building

Apps like this already exist, so the real question is why ours is still needed. Our answer is that the useful parts exist separately, and the apps that combine them don't seem to be used where our users play.

Our interviews point the same way. None of the three participants mentioned using any of these apps. They find partners through a local club chat, through friends or through a coach, and tournament results are shared in WhatsApp and Telegram groups, where messages get lost. One participant said his country has apps for finding basketball and football players but nothing for tennis. Another said an app would be useless if nobody nearby used it. That is exactly the problem a global app with no local users has.

So the case for our app rests on four things:

- It combines ratings, finding players and simple tournament tools in one place, for local amateur communities.
- It launches through existing clubs and groups, so each area has enough active players from the start.
- It gives informal organizers a simple way to publish brackets and results instead of posting them in chats.
- Ratings come from everyday community matches, confirmed by both players, not only from official events.

## Differences from our app and what we can learn

| System | Better than our app at | Missing for our users | Idea worth borrowing |
|---|---|---|---|
| UTR Sports | An established global rating, a large event network, a mature doubles rating | No local presence found. Events go through official providers. The 1.00–16.50 scale may feel complicated to casual players. | Keeping confirmed and unconfirmed results apart, and rating doubles teams by their average |
| Playtomic | Court booking and payment built in | Focused on padel. No clubs found in Kazakhstan. Tournament features not described. | Level ranges for open matches, and a reliability score for new players |
| GTN | A large community and court directory | Rating method not public. Key features cost money. No local presence found. | Ladders, as a possible later feature |
| WTN | Official and already shown in Kazakhstan | Only a rating, with no tools around it | Letting players enter their WTN as a starting level, and adjusting ratings after inactivity |
| TLTS | A known local tournament brand with access to courts | No way to find players, the rating method isn't published, website only | Level categories for tournaments. Also a possible partner for our launch. |

There is a risk to all this. If UTR or Playtomic builds an active community in Kazakhstan, our local advantage gets smaller. Connecting to them, for example by importing a UTR or WTN number, may then make more sense than competing.

## Limitations

This comparison is based on public information only. We didn't install the apps, so some "not found" cells may hide features that do exist. Our information about GTN comes from third-party pages, and their member numbers don't match. We also didn't check inside UTR's or Playtomic's search whether they have any events or clubs in Almaty or Astana. That is the next thing to check.

## Sources

1. UTR Sports, *Tennis app*: https://www.utrsports.net/pages/tennis-app
2. UTR Sports, *What is UTR Rating and how does it work?*: https://www.utrsports.net/back-to-basics-what-is-utr-and-how-does-it-work
3. UTR Sports, *Play tennis*: https://www.utrsports.net/pages/play-tennis
4. Universal Tennis Support, *FAQ: Doubles algorithm*: https://support.universaltennis.com/support/solutions/articles/9000183289-faq-doubles-algorithm
5. Playtomic Help, *How the Playtomic level system works*: https://playerhelp.playtomic.com/hc/en-gb/articles/43310980754193-How-the-Playtomic-level-system-works
6. Playtomic Manager Help, *How to configure Open Matches at your club*: https://helpmanager.playtomic.com/hc/en-gb/articles/20535035123473-How-to-configure-Open-Matches-at-your-Club
7. Tennishead, *Global Tennis Network*: https://tennishead.net/?p=125866
8. The Hive Index, *Global Tennis Network*: https://thehiveindex.com/communities/global-tennis-network/
9. LTA, *ITF World Tennis Number*: https://www.lta.org.uk/play-compete/competing/player-ratings-rankings/world-tennis-number/
10. ITF, *World Tennis Number: how do you get yours?* (30 Aug 2022): https://www.itftennis.com/en/news-and-media/articles/itf-world-tennis-number-how-do-you-get-yours
11. Kapital.kz, *Tennis League TS membership passes 200 players* (2024): https://kapital.kz/lifestyle/127182/kolichestvo-sport-smenov-tennisnoy-ligi-ts-prevysilo-200-chelovek.html
12. Tennis League TS, official website: https://tlts.kz
