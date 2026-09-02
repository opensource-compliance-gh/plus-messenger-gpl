# Plus Messenger: nine years of GPL code with no corresponding source

Free software runs on a bargain. Take my code, change it, sell it, build a business on it, and I will never ask you for a penny. In return, you pass the same freedom on to whoever receives what you built. That is the entire deal, and it is the only thing holding the ecosystem together.

This repository documents nine years of one developer taking the first half of that bargain and refusing the second, in an application with more than fifty million downloads, and what happened to the record when somebody pointed it out.

It is not a historical grievance. It is happening today. Every day this continues, fifty million people hold a copy of GPL-licensed software they have a right to inspect and cannot. Every day, the code that shows them adverts and takes their payments sits in a binary nobody outside the project has ever been permitted to read. And every few weeks somebody wanders into the support group, asks where the source is, and gets pointed at a pinned rule telling them not to ask. That has been the routine since 2016.

So I checked properly. It took an evening.

**Plus Messenger** (`org.telegram.plus`) is a fork of Telegram for Android, which is licensed GPL-2.0-or-later. The fork is entirely legitimate: the GPL exists to permit exactly this. It attaches one condition to handing someone the binary, which is that you also hand over the corresponding source, or a written offer to supply it.

The repository the rules point to has **three commits**. The last one containing code is dated **13 September 2017**. The version Google Play is serving today was built on **29 August 2026**, eight major versions and nine years later.

On its own that's a stale repository, and plenty of projects drift. Here is why it isn't that.

Pull the shipped APK apart and you find current Telegram code, including features that didn't exist before 2026, sitting alongside roughly **eleven thousand lines under `org.telegram.plus` that appear in no repository, at any version, ever**. That unpublished portion is not a rounding error or a build artifact. It is the advertising engine, the analytics pipeline and the Google Play Billing integration, and it sells ad removal from **EUR 5.99 to 99.99**. Search the app, the Play listing, the official site and both repositories for a written offer of source and you find a theme-preview joke string and an error message.

Then it gets worse, and the worse part is in Chapter 5.

Everything here is checkable. The exact binary is pinned by SHA-256, the commit history comes from an API anyone can query without an account, and [Chapter 12](#chapter-12-verify-all-of-it-yourself) is a copy-pasteable script that reproduces the technical case in about ten minutes. Where something is inference rather than fact, it says so in the sentence.

## About this record

This repository is a permanent, independently verifiable record of **continuous and unresolved non-compliance with the GNU General Public License v2 by Plus Messenger**, an Android application with more than fifty million Google Play downloads.

It documents, in one place and with primary sources attached to every claim:

1. The published source history, which stopped in September 2017.
2. Binary analysis of the version distributed in 2026, including the advertising, analytics and billing layer that appears in no repository at any version.
3. Ten years of source-code requests from users and developers, and the pinned rules that make the question off-topic in the app's own support groups.
4. The stated justification for withholding the source, and the developer's own conduct in October 2025 that contradicted it.
5. The formal compliance request, and the absence of any reply.
6. What happened to this record when it was reported, venue by venue.

The obligation at issue is not obscure or onerous. Section 3 asks a distributor of GPL code for one thing: the corresponding source, or a written offer to supply it. That obligation has gone unmet across eight major versions and nine years, while the application earned advertising and subscription revenue from code the public was never permitted to read.

Copyleft only functions if the source obligation is honoured by the people who benefit from it. This record exists so that a decade of declining to honour it is documented rather than forgotten, and so that anyone, now or years from now, can check every claim in it without trusting the author.

## Index

- **[Chapter 1: How Plus got here](#chapter-1-how-plus-got-here)**
- **[Chapter 2: What the licence actually requires](#chapter-2-what-the-licence-actually-requires)**
- **[Chapter 3: The published source stopped in 2017](#chapter-3-the-published-source-stopped-in-2017)**
- **[Chapter 4: The changelog says the source is being updated](#chapter-4-the-changelog-says-the-source-is-being-updated)**
- **[Chapter 5: The app contains code that has never been published](#chapter-5-the-app-contains-code-that-has-never-been-published)**
    - [What the unpublished code actually does](#what-the-unpublished-code-actually-does)
- **[Chapter 6: There is no written offer either](#chapter-6-there-is-no-written-offer-either)**
- **[Chapter 7: This is a written policy, not an oversight](#chapter-7-this-is-a-written-policy-not-an-oversight)**
- **[Chapter 8: October 2025, when the stated reason collided with reality](#chapter-8-october-2025-when-the-stated-reason-collided-with-reality)**
- **[Chapter 9: The same app, a different store, a different story](#chapter-9-the-same-app-a-different-store-a-different-story)**
- **[Chapter 10: What was done about it](#chapter-10-what-was-done-about-it)**
- **[Chapter 11: Testing the defences](#chapter-11-testing-the-defences)**
- **[Chapter 12: Verify all of it yourself](#chapter-12-verify-all-of-it-yourself)**
- **[Chapter 13: What happened when this was reported](#chapter-13-what-happened-when-this-was-reported)**
- **[Chapter 14: Wall of shame](#chapter-14-wall-of-shame)**
    - [14.1 vdbhb59 (`@flossboxin`)](#141-vdbhb59-flossboxin)
    - [14.2 Licaon_Kter](#142-licaon_kter)
    - [14.3 Oswald Boelcke, XDA Senior Moderator](#143-oswald-boelcke-xda-senior-moderator)
    - [14.4 F-Droid forum staff](#144-f-droid-forum-staff)
    - [14.5 The pattern](#145-the-pattern)
- **[Chapter 15: What remains unresolved](#chapter-15-what-remains-unresolved)**
- **[Chapter 16: Requested remediation](#chapter-16-requested-remediation)**
- **[Chapter 17: Conclusion](#chapter-17-conclusion)**
- **[A word to anyone deciding whether to install this, or anything like it](#a-word-to-anyone-deciding-whether-to-install-this-or-anything-like-it)**
    - [Notice](#notice)

## Document control

| Field | Value |
|---|---|
| **Subject** | Plus Messenger, package `org.telegram.plus`, developer "rafalense" |
| **Matter** | Non-compliance with GNU General Public License, version 2 (GPL-2.0-or-later), section 3 |
| **Upstream work** | Telegram for Android, © Nikolai Kudashov and contributors |
| **Binary examined** | 12.10.1.0, `versionCode 22490`, base APK SHA-256 `d332a130…fbbfef` |
| **Evidence captured** | 2026-09-01 and 2026-09-02 |
| **Rights holders notified** | 2026-09-01 |
| **Status** | Open. No response from the distributor. |
| **Author** | Pseudonymous. Not counsel, and none of this is legal advice. Every legal proposition is either a quotation from the licence or is flagged **[inference]**. |

## What the record shows

| What was found | Where |
|---|---|
| No corresponding source has been published for any release since 2017-09-13 | Chapter 3 |
| Release notes state "Source code updated to vX" against a repository with zero code commits since 2017 | Chapter 4 |
| The distributed binary contains an ad, analytics and billing layer (`org.telegram.plus`) absent from every published source tree | Chapter 5 |
| The unpublished layer is 11,440 lines including a Firebase Auth/Firestore backend and a push-triggered login-code retrieval path gated to two hardcoded numbers | Chapter 5 |
| No section 3(b) written offer exists in the app, on any store listing, or on the official site | Chapter 6 |
| Withholding the source is stated policy, pinned publicly since 2019-06-17, and enforced by group administrators | Chapter 7 |
| The stated justification for withholding (preventing others from adding advertising) was contradicted by the distributor's own conduct on 2025-10-02 | Chapter 8 |
| Monetisation is disclosed on Google Play and undisclosed on Huawei AppGallery, contrary to Telegram API ToS §3.2 | Chapter 9 |

## Standard applied

1. A statement of fact is accompanied by a URL you can open or an artifact you can recompute. It is not asserted otherwise.
2. Reasoning that goes beyond the primary evidence is marked **[inference]**.
3. Personal judgement is marked **[opinion]**.
3a. Applying licence text to facts is analysis, not fact. Chapters 2, 4, 6 and 16 contain legal reasoning. None of it is a court ruling and none of it should be read as one.
4. Where a defence exists, it is stated in its strongest form and then tested against the evidence. Chapter 11 does this for ten of them.
5. Quotations are verbatim, with the date and the source of each. Translations are given alongside the original, never in place of it.
6. Claims that could not be substantiated are absent. Where the evidence has a limit, the limit is stated next to the claim it affects rather than collected at the end.

---

# Chapter 1: How Plus got here

Plus Messenger is a modified build of **Telegram for Android**, with tabs, multiple accounts, chat categories and theming added. It is genuinely popular and has been maintained for over a decade.

| | |
|---|---|
| Package | `org.telegram.plus` |
| Developer | rafalense |
| Play installs | 50,000,000+ |
| Current version | 12.10.1.0, released 2026-08-29 |
| Upstream project | [DrKLO/Telegram](https://github.com/DrKLO/Telegram), © Nikolai Kudashov and contributors |
| Upstream licence | **GPL-2.0-or-later** |

The fork itself is completely legitimate. The GPL exists to permit exactly this.

### He has consistently presented the app as GPL-licensed

This matters because it removes the "he didn't know" reading. The representation is his own, in three places:

1. **His GitLab repository** carries the GPLv2 `LICENSE` file: [gitlab.com/rafalense/plus-messenger](https://gitlab.com/rafalense/plus-messenger) (profile: [gitlab.com/rafalense](https://gitlab.com/rafalense))
2. **His GitHub repository** carries it too: [github.com/rafalense/Plus-Messenger](https://github.com/rafalense/Plus-Messenger) (profile: [github.com/rafalense](https://github.com/rafalense))
3. **He submitted the app to F-Droid himself on 27 March 2015, describing it as "GNU GPL v2"**: https://f-droid.org/forums/topic/plus/

That submission was declined, and the recorded reason concerned bundled Google Play Services rather than the licence. **Remember it.** In Chapter 14, an F-Droid board member deletes this report on the grounds that it has nothing to do with F-Droid.

### Where he distributes the binary

He lists these himself, in his official FAQ post ([plusmsgrfaq/23](https://t.me/plusmsgrfaq/23), 2020-07-01):

1. **Google Play**, 50M+ installs: https://play.google.com/store/apps/details?id=org.telegram.plus, labelled "Contains ads" and "In-app purchases"
2. **Huawei AppGallery**, 6M installs: https://appgallery.huawei.com/app/C102568417. This listing becomes its own finding in Chapter 9.
3. **APKMirror**: `rafalense/plus-messenger`
4. **Telegram**: https://t.me/plusmsgrupdates
5. **Official site**: https://plusmessenger.org

Five distribution surfaces. **None of them offers source.** That single sentence is already a GPLv2 section 3 failure, repeated five ways for nine years, and it is the least serious finding in this document.

---

# Chapter 2: What the licence actually requires

Only the parts that matter to this case. GPLv2, section 3:

> **3.** You may copy and distribute the Program [...] in object code or executable form under the terms of Sections 1 and 2 above provided that you also do one of the following:
>
> **a)** Accompany it with the **complete corresponding** machine-readable source code [...]; or,
>
> **b)** Accompany it with a **written offer**, valid for at least three years, to give **any third party** [...] a complete machine-readable copy of the corresponding source code [...]
>
> [...] For an executable work, **complete source code means all the source code for all modules it contains**, plus any associated interface definition files, **plus the scripts used to control compilation and installation** of the executable.

And section 4, the consequence:

> **4.** [...] Any attempt otherwise to copy, modify, sublicense or distribute the Program is void, and **will automatically terminate your rights** under this License.

Section 3 has a third option, **3(c)**, which permits passing along the written offer you yourself received. It applies only to noncommercial redistribution of something you did not originate, so it is unavailable to the party who created and distributes the work. It is noted here for completeness, because a reader checking the licence text will find it.

Four words do all the work here:

| Word | What it means | What it rules out |
|---|---|---|
| **complete** | all modules, plus build scripts | publishing the parts you don't mind sharing |
| **corresponding** | the source of the binary you shipped | publishing an older version instead |
| **any third party** | a 3(b) offer is open to everyone | an offer to a list you approve |
| **accompany** | it travels with the binary | "eventually", or "on request, maybe" |

The test is therefore:

> **What the licence requires → what he distributes → what he provides → where the mismatch is.**

Hold those four words. Chapter 7 is his own support infrastructure explaining, in writing and pinned for seven years, that the source is *delayed*, *partial*, and *available to limited entities such as Telegram*.

---

# Chapter 3: The published source stopped in 2017

His own group rules point users to the GitLab repository as the current one. Here is its complete history, not a selection of it:

```
0978c068   2017-09-13   Add readme.md
1d961518   2017-09-13   Update to v4.2.1.1        <-- last commit containing code, ever
b418c867   2019-02-07   Update README.md          <-- documentation only
```

Fetch it yourself with no account:

```
https://gitlab.com/api/v4/projects/4142452/repository/commits
```

The project has never tagged a release. The `build.gradle` in that tree carries `versionCode 1047`, which is the 4.2.1.1 era, September 2017. The GitHub repository is not a fallback either, being older still at v2.5.2.1 with its last code commit on 2015-03-11.

Two people already noticed and filed the obvious issue. Both cite the licence, and both have sat open since **October 2018** without a reply:
   - https://gitlab.com/rafalense/plus-messenger/-/issues/20
   - https://gitlab.com/rafalense/plus-messenger/-/issues/22

| | Version | Date |
|---|---|---|
| Newest source ever published | **4.2.1.1** | 2017-09-13 |
| Currently shipping on Google Play | **12.10.1.0** | 2026-08-29 |

That is eight major versions across nine years, and section 3 requires source corresponding to the binary being distributed. There is none for anything released since 2017.

No corresponding source has been published for any release in nine years. Nothing more yet: at this stage, a solo developer with a stale repository is still a plausible reading.

It survives about another ten minutes. [Chapter 4](#chapter-4-the-changelog-says-the-source-is-being-updated) is what breaks it, and the strongest counter-argument available here, that the published source may correspond to an archived 2017 build, is tested in [Chapter 11](#chapter-11-testing-the-defences).

---

# Chapter 4: The changelog says the source is being updated

### What was claimed

Every release note carries a line that reads like ongoing compliance:

> *"New in version 10.0.5.0: **Source code updated to v10.0.5**."*
> Source: [plusmsgr/377](https://t.me/plusmsgr/377), 2023-09-07

> *"New in version 12.2.10.0: **Source code updated to v12.2.10**."*
> Source: [plusmsgr/465](https://t.me/plusmsgr/465), 2025-12-10

> *"#stable · **Source code updated to v12.2.10**."*
> Source: [plusmsgrupdates/101](https://t.me/plusmsgrupdates/101), 2025-12-10

This is why a great many users in his support groups sincerely believe the app is open source, and say so in public.

### What the evidence shows

Chapter 3. **Zero code commits since 2017.**

Both statements cannot describe the same event.

### Why those two things do not match

He explains the phrase himself, twice, unprompted:

> *"...**Telegram v10.12 source code has to be published**. Last source code update was a month ago, ...v10.10."*
> Source: [plusmsgr/400](https://t.me/plusmsgr/400), 2024-05-02

> *"Plus Messenger will be updated to v11.6.2 **as soon as Telegram releases source code** based on that version."*
> Source: [plusmsgr/431](https://t.me/plusmsgr/431), 2025-01-21

He is waiting for **Telegram** to publish **Telegram's** source so he can merge it into **his private tree**. "Source code updated to v12.2.10" describes an upstream merge he performed. It is not a release he made.

### What this establishes

The phrase is literally true and functionally misleading. It appears where a user would look for a source release, phrased as a source release would be phrased, in the changelog of an app whose repository has not moved since 2017.

**[inference]** I cannot prove intent and will not try. What is proven is the effect: users read it as compliance, and it is not compliance.

A stale repository is a backlog. A stale repository with a monthly "source code updated" line in front of it is a different thing, and this is the point where the charitable reading gets difficult.

---

# Chapter 5: The app contains code that has never been published

Everything so far concerns what is *missing*. This is what is *shipped*, and it is where the case stops being about tidiness. Measure it against the four words in [Chapter 2](#chapter-2-what-the-licence-actually-requires): this chapter establishes what "corresponding" has to cover, [Chapter 6](#chapter-6-there-is-no-written-offer-either) shows that the alternative route of a written offer was not taken either, and [the section on what that code does](#what-the-unpublished-code-actually-does) examines what the unpublished code does once it is running.

### What I found, in plain English

The app on Google Play contains two kinds of code. Telegram's, covered by the GPL, including features that did not exist before 2026. And his own, which has never appeared in any repository at any version, and which is the part that shows you adverts and takes your money.

That second category is an advertising engine, an analytics pipeline and a payment system, and none of it can be read by anyone outside the project.

### Evidence

**1. The exact artifact.** Identified precisely enough that any disagreement becomes a factual question rather than an argument.

Plus Messenger **12.10.1.0**, `versionCode 22490`, `compileSdk 36 / targetSdk 36`, obtained 2026-09-01 as an XAPK bundle from APKPure, one of the mirrors that redistributes the Play build. The acquisition source is stated because it matters: this is a mirror copy of the Play artifact, identified by hash, not a capture taken directly from Google Play.

```
XAPK bundle                      87,575,235 bytes
  SHA-256  62a705cf7294121ee7b1a5aef638835cc140346289d756d2f4d35f1eefec10d6

base APK org.telegram.plus.apk   68,311,725 bytes
  SHA-256  d332a1304fc0c0c3daecc8fe7321893f7a6e88ffb59916743d175bf626fbbfef
```

**2. It is the genuine distributed artifact, not a third-party repack.**

```
Signature schemes v1 + v2 + v3         verified
V3 signer certificate  SHA-256  6ebb622268aad319dbe8a1f414837d2843a9b35856aefb7dee2971a3d493f276
V3 signer public key   SHA-256  6ef39e017590a79c5bf5c19eeefc9aeb49d4d60bcb2d5e214414b0efe382df9e
Play App Signing stamp SHA-256  3257d599a49d2c961a471ca9843f59d341a405884583fc087df4237b733bbd6d
```

Two things follow, and it is worth being precise about which. The APK carries a **Play App Signing source stamp**, and its app-signing certificate is the one Google Play serves for `org.telegram.plus`. That establishes the artifact came through the official distribution pipeline for this package: not a repack, not a mirror's modification, not somebody else's tampering.

It does **not** establish that the developer personally performed the signing. Under [Play App Signing](https://developer.android.com/studio/publish/app-signing), Google holds the app signing key and signs the delivered artifact from an uploaded bundle. What is attributable to him is what he uploaded and distributes under his account, which is all any argument here requires.

**3. It is running current Telegram code, not 2017 code.** Six dex files, dominated by upstream classes:

```
org/telegram/tgnet/TLRPC*                    3,851 references
org/telegram/tgnet/tl/TL*                    1,878
org/telegram/ui/ChatActivity*                  978
org/telegram/messenger/MessagesController      657
org/telegram/ui/Stars/StarGiftSheet             324
```

`StarGiftSheet` is a **2026** upstream feature. The binary is not carrying 2017-era Telegram that happens to match a 2017-era repository. The corresponding source is *current Telegram plus his modifications*, and the published tree is neither.

**4. The layer that has never been published.**

```
org/telegram/plus/ads/AdsController             954 references
org/telegram/plus/helpers/FirebaseHelper        636
org/telegram/plus/ads/RemoveAdsBottomSheet      530
org/telegram/plus/ads/AdsInstance               502
org/telegram/plus/SafeModeActivity              317
org/telegram/plus/ads/BillingHelper             306
org/telegram/plus/ui/drawer/*
org/telegram/plus/update/UpdateAppAlertDialog
```

Shipped alongside it: `com.google.android.gms.ads` (AdMob), `com.google.firebase.analytics`, `com.android.billingclient` (Google Play Billing).

**5. The same paths in the published source.** The published tree at `org/telegram/` contains exactly five directories: `PhoneFormat`, `SQLite`, `messenger`, `tgnet`, `ui`.

```
org/telegram/plus                            ->  HTTP 404
org/telegram/plus/ads/AdsController.java     ->  HTTP 404
org/telegram/messenger/plus                  ->  HTTP 404
```

**6. What that code does to the user.** The in-app **Ads** screen offers Remove Ads, an Enable Ads toggle, Ad placement, and Check Purchases. The purchase sheet sells:

| Item | Price |
|---|---|
| Remove ads (Plus Messenger) | **EUR 5.99** |
| Remove ads & Donate | EUR 11.99 |
| Remove ads & Donate | EUR 24.99 |
| Remove ads & Donate | EUR 49.99 |
| Remove ads & Donate | **EUR 99.99** |

String resources include `AdsRemoved` and the sales line *"Remove ads and support Plus Messenger project with the approximate price of a coffee/pizza"*, next to copy thanking users for *"all these more than 10 years of free Plus Messenger development"*.

### What this establishes

**The APK contains `org/telegram/plus/ads/*` while the published source does not contain it, in any version, in either repository.** There is no old copy of this code. There is no copy.

The specific components that convert a messaging client into a revenue stream are the specific components that have never been released.


---

## What the unpublished code actually does

Everything above establishes that the code exists and was never published. This section is about what is in it, and it is the point where the licence stops being a formality. This section is the basis for the warning at the end of this document, and for the argument in [Chapter 17](#chapter-17-conclusion) that the cost of withheld source is measured in what nobody can check.

**Decompiled 2026-09-02 from the same base APK** (`d332a130…fbbfef`, hash re-verified before decompilation) with `jadx`. The `org.telegram.plus` package contains **39 source files and 11,440 lines** of code that appear in no repository.

### What it contains

It is a full backend integration rather than an advertising shim:

| Component | What it is |
|---|---|
| `FirebaseAnalytics`, `FirebaseCrashlytics` | Telemetry, with app version set as a user property |
| **`FirebaseAuth`** | Anonymous sign-in to the developer's Firebase project |
| **`FirebaseFirestore`** | A cloud database the app reads from and writes to |
| Firebase Remote Config | Server-controlled behaviour, with a configurable fetch interval |
| Firebase Cloud Messaging topics | Push subscription and a push **command handler** |
| `ads/*`, `BillingHelper` | AdMob, and the Play Billing purchase flow |
| `PlusUpdater`, `UpdateAppAlertDialog` | A self-update mechanism outside the store |
| `PlusContentProvider`, `WearProvider` | Exported Android components |

### The part that matters

`FirebaseHelper` contains a hardcoded array named `test_ids`: **two Spanish mobile numbers, stored Base64-encoded** in the binary. They are not printed in this document, because they are personal data and publishing them serves no purpose. Anyone reproducing the decompilation will find them in seconds, and the check that uses them is `isTestId()`.

When the signed-in account's phone number matches one of those two, the app will:

1. Read the **last 20 messages from Telegram peer `777000`**, which is Telegram's official service-notifications account, the account that delivers login codes.
2. Regex-scan them for a 5 to 8 digit code.
3. Write that code, Base64-encoded, into a **Cloud Firestore collection named `tokens`**, in a document named after the account's own phone number, with a server timestamp.

It can also be triggered remotely. `readTopic()` handles incoming push messages, and a push whose payload contains `login` carries `phone` and `code` fields. On such a push, gated by the same two-number check, the app either injects a code into the login flow or kicks off the harvest above.

To feed it, **upstream Telegram's `PushListenerController` was modified in eight places** to pass incoming push text through `FirebaseHelper.isLoginCode()`.

### What this establishes, precisely

**Fact.** The shipped binary contains a remotely triggerable mechanism that reads Telegram login codes out of the user's own message history and uploads them to the developer's Firebase project, and it required modifying upstream GPL code in eight places to wire up.

**Fact.** That mechanism is gated behind a client-side comparison against two hardcoded phone numbers. For any other account, `isTestId()` returns false and nothing is read or uploaded.

**[inference]** This is very probably a developer automation harness for his own test accounts, not a mechanism aimed at users. That is the most plausible reading and I am not going to claim otherwise.

**And that is exactly the point.** Every one of those 50,000,000 installs carries the scanner, the Firestore upload path, the push command handler and the modified upstream push controller. The only thing standing between that machinery and any given user is an `if` statement comparing their phone number against a list, in a build that is remotely configurable, in code the licence required him to publish nine years ago and which nobody outside has ever been able to read.

Nobody is alleging he has done anything with it. Nobody **can** allege anything either way, and that is the injury. This is what the GPL's source requirement is actually for: not tidiness, not credit, but so that the 50 million people running a messaging client can find out what it does. Somebody reading the source would have found this in an afternoon. Instead it sat unreviewed for as long as it has existed.

### What this looks like in plain language

The class inventory above doesn't really convey it, so here it is the way I'd explain it to someone over a beer.

I downloaded the app that fifty million people have installed. I ran a decompiler over it. Out came eleven thousand lines of code that has never been published anywhere, and sitting inside it:

1. A live connection to a cloud database the app both reads from and writes to.
2. Anonymous sign-in to the developer's Firebase project, so the app authenticates itself to that backend without the user being asked or told.
3. A remote configuration channel, so what the app does can be changed after you install it, without shipping an update through the store.
4. A push handler that accepts instructions, not just notifications.
5. Its own updater, capable of pulling a new version outside the Play Store.
6. A routine that reads your Telegram service messages, pulls the login code out of them, and writes it to that cloud database in a document named after your phone number.

Number six only fires for two hardcoded phone numbers. I have now said that three times and I will keep saying it every time it comes up, because it's true, and because it's the whole difference between a test harness and something far uglier.

Now look at the rest of the list again. A messaging client with fifty million downloads is carrying a remotely configurable command channel, an authenticated backend connection and an out-of-store updater, in code nobody outside one person has ever read, that the licence has obliged him to publish since 2017.

None of that is illegal, and plenty of apps ship Firebase. That isn't the point. The point is that these capabilities are precisely the parts he never published, in an app whose users spent a decade being told it was open source, and every one of them is the kind of thing a reviewer would want to look at first.

### Why this is not a hypothetical concern

Five months before this record was compiled, a different Telegram fork demonstrated exactly the risk being described.

On 2026-04-03 it was [reported on r/Android](https://www.reddit.com/r/Android/comments/1sb3h81/nekogram_caught_collecting_user_account/) that **Nekogram** was sending users' phone numbers and usernames to a developer-controlled Telegram bot, via, in the reporter's words:

> "obfuscated injected code **that is not in the source code provided on GitHub**. The packaged APK with the malicious code is distributed via Play Store, GitHub Releases and their Telegram channel."

The report states the developer acknowledged it. A related technical discussion is at [net4people/bbs issue 601](https://github.com/net4people/bbs/issues/601). Readers should evaluate that case on its own evidence; it is cited here for one narrow point, not as a finding of this document.

**The narrow point.** Nekogram publishes source. That is *why* somebody could compare the published source against the shipped APK, find the difference, and raise it. The discovery mechanism was a diff.

Plus Messenger cannot be checked that way. There is no current source to diff against, and has not been since 2017. The only reason the material described there is documented here at all is that it was decompiled by hand from a binary, which is slow, lossy, and something almost nobody does.

**To be explicit, because the distinction matters:** nothing in this document alleges that Plus Messenger does what Nekogram was reported to have done. The login-code path described above is gated to two hardcoded numbers, and for every other account it does nothing. The comparison is about *auditability*, not about conduct.

That is the answer to anyone who regards a nine-year source gap as a paperwork problem. In the same ecosystem, in the same year, in an app of the same type, the published-source requirement is what surfaced a real privacy incident. The app that published source got audited. The app that never published source, with fifty million installs, has never been audited by anyone, and would not be now if somebody had not spent an evening running `jadx`.


---

# Chapter 6: There is no written offer either

Section 3 offers an alternative to shipping a source tarball with every download: a written offer to supply it on request, quoted in full in [Chapter 2](#chapter-2-what-the-licence-actually-requires). It was not used either. What using it would involve is set out in [Chapter 16](#chapter-16-requested-remediation).

The decoded app resources were searched for "GNU General Public License", for "source code", and for repository URLs. The complete set of results:

1. A theme-preview joke string.
2. An error message about waiting for Telegram to update its source code.

First-party screenshots of the running app confirm that Settings terminates at a version number, and the Help section contains no licence or source entry. The Play listing carries no source link. `plusmessenger.org` carries no source link.

There is no section 3(a) compliance (no corresponding source) and no section 3(b) compliance (no written offer). Both routes the licence provides are unused.

Those two strings are the entire licence footprint of an application built on GPL code and installed fifty million times.

---

# Chapter 7: This is a written policy, not an oversight

One stale repository is an accident. This is the chapter where that reading stops working, and the rule quoted below is what [Chapter 8](#chapter-8-october-2025-when-the-stated-reason-collided-with-reality) then measures the developer's own conduct against.

### 2016: the violation is identified correctly, in his own group, with him in it

Ten years ago, in the Spanish support group:

1. [TodoSobrePlusMessenger/7621](https://t.me/TodoSobrePlusMessenger/7621) (2016-09-06): *"supuestamente todas son gpl, pero sacan el código de las que les da la gana y cuando quieren"*
2. [/7623](https://t.me/TodoSobrePlusMessenger/7623) (2016-09-06): going closed-source would "look bad", so they don't, while being held up as a free-software example, *"y no es cierto"*
3. [/10640](https://t.me/TodoSobrePlusMessenger/10640) (2016-09-23): *"si tu quieres conocer el codigo **tienes el derecho a pedirselo** y ellos, al estar bajo cierta licencia, **deben dartelo**"*
4. [/14402](https://t.me/TodoSobrePlusMessenger/14402) (2016-10-05): proposes that Telegram cut off API access for apps that do not honour the licence

The developer is in that group and is addressed directly at [/2718](https://t.me/TodoSobrePlusMessenger/2718) (2016-04-20).

Someone worked out both the violation and the enforcement lever in 2016. Nothing happened. Note item 4 in particular. Chapter 9 is that idea, ten years later, finally filed.

### 2017: a group admin concedes it in writing

> *"La GPL...actualmente **no se cumple**. Pero al ser una licencia basada en copyright solo los Autores del propio código o entidades validados por los autores pueden llevar a acciones legales..."*
> Source: [TodoSobrePlusMessenger/36632](https://t.me/TodoSobrePlusMessenger/36632), 2017-10-21, admin FabianPastor

*The GPL is currently not being complied with, but only the copyright holders can act on it.* Both halves are correct, and the second half is why the first half held for another nine years. It is also, almost word for word, the conclusion this investigation reached independently in 2026.

### 2019: withholding the source becomes pinned policy

The Spanish group's rules have been **pinned since 2019-06-17**: [TodoSobrePlusMessenger/56212](https://t.me/TodoSobrePlusMessenger/56212)

Under the heading *"Código Fuente / Source Code"*:

> *"La última versión del código está accesible a **entidades limitadas como Telegram**... el dev de Plus Messenger **retrasa la liberación del código** para evitar que terceros desarrolladores usen el codigo... **en su propio beneficio AGREGANDO PUBLICIDAD** y otros regalos sin nisiquiera dar crédito..."*

and, in the same pinned message:

> *"**Este no es el lugar para preguntar sobre el código fuente.**"*
> (This is not the place to ask about the source code.)

The English rules say the same and are pinned at [plusmsgrchat/1958625](https://t.me/plusmsgrchat/1958625) (2026-01-14).

Now put that pinned text against the four words from Chapter 2:

| The pinned rule says | Section 3 says |
|---|---|
| release is **delayed** | there is no delay clause |
| accessible to **limited entities such as Telegram** | 3(b) offers must be open to **any third party** |
| **this is not the place to ask** | there is no such place, and that is the design |

### The rule is enforced, in English, by an admin

> *"**This is not the place to ask for source code.** Please read the group rules again."*
> Source: [plusmsgrchat/1798149](https://t.me/plusmsgrchat/1798149), 2025-01-22, admin Prowler

### People asked anyway, for ten years

| Date | Source | What was asked |
|---|---|---|
| 2021-07-23 | [plusmsgrchat/1005599](https://t.me/plusmsgrchat/1005599) | *"I would like to get an up-to-date source code for Plus Messenger 7.8.0-7.8.2. **Can you share according to your license?**"* |
| 2022-03-10 | [plusmsgrchat/1175604](https://t.me/plusmsgrchat/1175604) | volunteer: *"Latest source is here <gitlab>. **Newer source isn't released yet**, please read the pinned message"* |
| 2022-06-23 | [plusmsgrchat/1231196](https://t.me/plusmsgrchat/1231196) | *"...source is no longer updated... **Meaning it violates the GPL license.**"* |
| 2023-02-19 | [TodoSobrePlusMessenger/208400](https://t.me/TodoSobrePlusMessenger/208400) | a developer checks both repos, both stale, asks for a newer one |
| 2024-12-14 | [TodoSobrePlusMessenger/228653](https://t.me/TodoSobrePlusMessenger/228653) | *"¿alguien sabe dónde está el código fuente?"* → same user: *"**Vamos que no es de código abierto.** Gracias."* |
| 2025-05-07 | [plusmsgrchat/1840961](https://t.me/plusmsgrchat/1840961) | a developer wanting to build on it: *"the gitlab one is 6+ years old and the github one is 10+ years old"* |
| 2025-09-01 | [plusmsgrchat/1893817](https://t.me/plusmsgrchat/1893817) | *"How come there isn't a Github for plus messenger? **Is this really closed source?**"* |
| 2026-04-08 | [plusmsgrchat/1992531](https://t.me/plusmsgrchat/1992531) | *"How can i see the source code,"* |
| 2026-05-13 | [plusmsgrchat/2002874](https://t.me/plusmsgrchat/2002874) | volunteer dbsergey: *"Developers of official app should share source code of 12.7 version first"* |

The last deflection is from May 2026. It is the same answer given in 2022, which is the same answer given in 2016.

### What this establishes

Ten years, two languages, at least a dozen different people, several of them developers who wanted to build on the app and gave up. A rule pinned for seven years declaring the question off-topic. An admin enforcing it in writing.

**[inference]** This is not a backlog. It is a policy operating as designed.

**One limit, stated because omitting it would be dishonest:** deleted messages cannot be counted. A deleted message is absent from any export by definition. What is proven here is the rule that makes the question bannable, plus the requests that survived and were deflected. No claim is made about how many were removed.

---

# Chapter 8: October 2025, when the stated reason collided with reality

### What was claimed

From the rule pinned since 2019, quoted in full above. The source is withheld to stop third-party developers from using the code:

> *"**en su propio beneficio AGREGANDO PUBLICIDAD**"*
> (for their own benefit, by adding advertising)

### What the evidence shows

**2 October 2025, 11:42.** His own channel:

> *"Plus Messenger will soon begin showing ads. After more than 10 years of completely free development, this step is necessary to ensure the project's sustainability and continuity. **A small one-time payment will be available to permanently remove [ads]**"*
> Source: [plusmsgr/458](https://t.me/plusmsgr/458) (Spanish: [plusmsgres/436](https://t.me/plusmsgres/436), 11:45)

### Why those two things do not match

He added advertising for his own benefit.

The precise act that the withheld source was said to be preventing is the act he performed, using code nobody else can read, in a market nobody else can enter, **because he withheld it**. The stated justification did not fail. It worked exactly as written, for one person.

Users noticed the price before they noticed the irony:

1. [/235555](https://t.me/TodoSobrePlusMessenger/235555) (2025-10-30): *"e pagado para quitar los anuncios pero no se quitan"*
2. [/236619](https://t.me/TodoSobrePlusMessenger/236619) (2025-11-26): paid, then received a Google auto-refund
3. [/237096](https://t.me/TodoSobrePlusMessenger/237096) (2025-12-10): *"he pagado por quitar los anuncios pero...siguen saliendo"*
4. [/237585](https://t.me/TodoSobrePlusMessenger/237585) (2025-12-30): *"ahora...para quitar los anuncios tienes que pagar"*

### And eight months later, the official responder still called it free

> *"**Plus Messenger is not a commercial project**, developer makes it on his own free time and **releases it for free**."* (followed by a donation link)
> Source: [plusmsgrchat/2012183](https://t.me/plusmsgrchat/2012183), 2026-06-11

Callback to Chapter 5: at the moment that message was being served to users, the shipped binary contained an AdMob integration, a Firebase analytics pipeline, a Play Billing client, a five-tier price ladder topping out at EUR 99.99, and a purchase-restore button.

**[opinion]** If that is not a commercial project, the phrase has no meaning left in it.

---

# Chapter 9: The same app, a different store, a different story

This one has nothing to do with copyright. It is the only lever here that works without a copyright holder lifting a finger, which matters because [Chapter 10](#chapter-10-what-was-done-about-it) shows every copyright-based route is closed to third parties. The store in question is the second one listed in [Chapter 1](#chapter-1-how-plus-got-here).

### What I found

Telegram's API Terms of Service, section 3.2, require that you *"clearly mention all the methods of monetization that are used in your app **in all its app store descriptions**."*

### Evidence

| Store | Version | "Contains ads" | "In-app purchases" |
|---|---|---|---|
| Google Play | 12.10.1.0 | **Yes** | **Yes** |
| Huawei AppGallery `C102568417` | 12.7.3.1, updated 2026-06-11 | **No** | **No** |

Both listings captured 2026-09-01. The AppGallery listing carries 6M installs, a "Free" price tag, a plain feature list, and marketing copy stale enough to still claim *"More than 20 million downloads"* and *"One of the best rated messaging apps on Play Store."*

Ads launched around October 2025, and the AppGallery listing was updated in June 2026 without disclosing any.

**The limit of this finding, stated plainly.** The AppGallery package itself was **not** downloaded or examined. Only the Play-lineage 12.10.1.0 artifact was. Huawei could in principle be receiving a different build without AdMob or Play Billing, which would make the listing accurate for that build and dispose of this finding entirely. Nothing in the record suggests that, and the developer describes one app across all channels, but it was not checked and is therefore not asserted.

### What this establishes

The same app, by the same developer, carries monetisation labels in one store and none in the other. **[inference]** If the AppGallery build ships the same ad and billing layer, that is a section 3.2 discrepancy on its face. Confirming it requires obtaining and inspecting the AppGallery package, which anyone with an AppGallery account can do and which this record has not done.

### Why it matters more than it looks

Unlike the copyright question, **anyone** can raise this with Telegram at `abuse@telegram.org`. Telegram controls API access for third-party clients, so it holds a practical lever that does not require a court. Not a lawsuit. Not a rights-holder form. It does not require Nikolai Kudashov to feel motivated on a particular Tuesday.

Somebody in that Spanish group worked this out in [2016](https://t.me/TodoSobrePlusMessenger/14402).

---

# Chapter 10: What was done about it

The technical case above was compiled on 2026-09-01 and put to the parties who can act on it, before any part of it was made public. Notification came first; publication came second. That order matters, and it is why this chapter exists.

### Who was notified

1. **The upstream copyright holders.** Telegram, and Nikolai Kudashov personally. They are the only parties who can bring an action or compel a store removal, so they were told first, privately, with the full evidence and a ready-to-file copyright notice they could use or discard.
2. **Licence enforcement organisations.** The bodies that exist for exactly this, given the same evidence and asked whether the analysis holds.
3. **The developer himself**, on his own issue tracker, in public: [issue 84](https://gitlab.com/rafalense/plus-messenger/-/issues/84), opened 2026-09-01 22:16 UTC. It doubles as a formal GPLv2 section 3 source request.
4. **Telegram's abuse channel**, separately, for the section 3.2 disclosure breach in Chapter 9.

Specific recipients, addresses and correspondence are deliberately not listed here. They are not evidence of anything the developer did, and publishing a contact list serves no purpose except to invite people to add to somebody's inbox.

### What was asked for

One thing, in every message: **publish the complete corresponding source for the version currently shipped, or ship a written offer.** No damages. No takedown demand. No apology.

### What came back

From the developer: **nothing.** Issue 84 has no reply, which places it alongside issues 20 and 22 from 2018.

Version 12.10.1.0 remains on Google Play, with the same unpublished ad layer, at the same prices.

### The doors that turned out to be locked

This part is published in full, because it is the part that matters to anyone who ever tries to report a licence violation. Every route below was tested live on 2026-09-01. None was assumed.

**Google Play's "Report a policy violation" form.** Selecting the category "Intellectual property" produces the message *"You will not be able to submit this form"* and redirects to the DMCA troubleshooter. The anyone-can-file IP report does not exist in practice.

**Google Play's "Flag as inappropriate".** Six fixed reasons, no free-text field:

1. Content was disturbing
2. Should be for mature audiences only
3. Content felt hostile
4. App felt suspicious
5. I disliked the ads
6. App wasn't what I was looking for

None describes a licence violation. The old "Other objection" box with a description field is gone. Nothing was submitted, because filing under a false reason would be worse than filing nothing.

**The DMCA route.** Rights-holder only, sworn identity, forwarded to the developer, published to Lumen. Correct for a copyright holder, unusable for anyone else, never filed.

**A public issue on the upstream repository.** DrKLO/Telegram has issues *and* discussions disabled. The GitHub API returns `has_issues=false`, `has_discussions=false`. There is no public way to tell the copyright holder anything on his own tracker.

### What this establishes

This chapter is also why the record went public at all. With every formal channel either closed or unanswered, publication was the remaining option, and [Chapter 13](#chapter-13-what-happened-when-this-was-reported) is what happened next.

**[inference]** This is the actual explanation for nine years, and it is neither apathy nor conspiracy. Enforcement depends entirely on one busy copyright holder, and the store distributing the app has closed every channel through which anybody else could file a report.

Nothing malfunctioned. Every part of that system did exactly what it was built to do, and the result is a nine-year violation with no door to report it through.

---

# Chapter 11: Testing the defences

Every argument below is the strongest version I can construct in his favour, not a straw man. Each is then tested against the evidence.

### "Could this simply be a misunderstanding of the licence?"

It would be a reasonable defence for a first-time contributor. It does not fit this record. He shipped a GPLv2 LICENSE file with both repositories, submitted the app to F-Droid as "GNU GPL v2" in 2015 (Chapter 1), and his support group has carried a pinned explanation of *why* the source is withheld since 2019 (Chapter 7). A pinned rationale for withholding is not a misunderstanding. It is a position.

### "Could the published repository correspond to a different build that is still distributed?"

Partly, and it is the fairest point available to him. The published tree is `versionCode 1047` (v4.2.1.1, 2017), and APK archive sites retain historical builds, so the published source may well correspond to an archived 2017 binary that is still downloadable somewhere.

That defence succeeds exactly as far as it goes and no further. Section 3 requires source corresponding to **the binary you distribute**. Google Play serves 12.10.1.0. Source matching a 2017 build discharges the obligation for the 2017 build and nothing after it. Every release from 2017-09-14 onward remains unaccompanied.

### "Could the missing material be legally excluded from 'corresponding source'?"

Section 3 excludes only *"anything that is normally distributed with the major components of the operating system"*. `org.telegram.plus.ads.AdsController` is not a component of Android. It is first-party application code, written by the distributor, running in his process, in his package namespace, driving his revenue. The AdMob and Billing libraries themselves are third-party dependencies and are not the claim here. The claim is his own 954-reference controller class that calls them.

### "Could generated or build-artifact files explain the discrepancy?"

No. Generated files would appear in the binary and be absent from source, which is normal and expected. What is absent here is the entire `org/telegram/plus` package tree: an ads controller, a billing helper, a purchase bottom sheet, a Firebase helper, a drawer UI package and an updater. Those are authored source files, not build output. And section 3 explicitly requires *"the scripts used to control compilation and installation"*, so even a pure build-system argument fails on the same sentence.

### "Does Telegram's own licensing situation change the analysis?"

No, and this is his stated defence, so it deserves the fullest answer. Telegram publishes its Android source. He has said, in his own words, that he waits for them ([plusmsgr/431](https://t.me/plusmsgr/431)). But section 3's obligation attaches to *whoever distributes the binary*. Upstream's schedule affects when he can rebase. It has no bearing on whether he publishes **his own** `org.telegram.plus` package and build scripts, which are his work, in his possession, right now. The excuse also has an expiry date it passed long ago: Telegram published throughout 2018 to 2026, and he published nothing.

### "Is there another source archive somewhere that I missed?"

This was checked, not assumed. His own FAQ post lists his official channels (Chapter 1) and none offers source. His own group rules label the 2017 GitLab repository *"Gitlab [Actual]"*, meaning current. Volunteers answering source questions in 2022 and 2026 pointed to that same repository. If a newer archive exists, the developer, his rules and his volunteers are all unaware of it. **If one is produced, this document will say so.**

### "Was he actually given an opportunity to comply?"

Yes, repeatedly, by many people over ten years (Chapter 7), and formally on 2026-09-01 at [issue 84](https://gitlab.com/rafalense/plus-messenger/-/issues/84) on his own tracker, alongside the unanswered requests from 2018. The remedy requested was publication and nothing else.

### "Could he hold separate permission, or a licence other than the GPL?"

This is the strongest defence available to him, and the document would be dishonest not to state it. A fork's author can hold a separate agreement with upstream rights holders, or a licence on terms other than the GPL, in which case section 3 would not constrain him in the way argued here.

Nothing in the public record indicates any such arrangement: the repositories carry the GPLv2 LICENSE file, the app was represented as GPLv2 in 2015, and the support group's rules discuss the source in licence terms rather than pointing to a private grant. But an arrangement of that kind would not necessarily be public, and only the developer or the rights holders can confirm or exclude it.

**Every conclusion in this document is therefore conditional on no such permission existing.** If it does, saying so would resolve the entire matter faster than publishing the source, and this record would be corrected the same day.

### "Is any part of this based only on inference?"

Four things, and each is marked where it appears:

1. That "Source code updated to vX" *functions* as a deflection (Chapter 4). What is proven is the wording, the zero commits, and his own explanation of what he means by it.
2. That the pattern is policy rather than backlog (Chapter 7). What is proven is the pinned rule, its stated rationale, and ten years of deflected requests.
3. That the enforcement vacuum, rather than apathy or coordination, explains the nine years (Chapter 10). What is proven is that each reporting route was tested and found closed.
4. That section 4 has terminated the licence (Chapter 16). No court has ruled on it.

Everything else is a link or a hash.

### "Only the copyright holder can complain, so why is a third party doing this?"

Only a copyright holder can sue or force a takedown. Correct, which is exactly why Kudashov and Telegram were notified first, before any of this was public. But section 3 gives **every recipient of the binary** a right to the corresponding source or to an offer good for any third party. Every recipient of the binary holds that right. That is not standing to sue. It is standing to ask and be answered.

### "It is one person working in his spare time. Leave him alone."

The GPL explicitly permits selling. Whether he may earn money from this is not in question and never has been. It attaches one condition, and he has not met it in nine years, while charging up to EUR 99.99.

---

# Chapter 12: Verify all of it yourself

Nothing here asks for trust. Roughly ten minutes, start to finish. Step 1 checks [Chapter 3](#chapter-3-the-published-source-stopped-in-2017), steps 2 and 3 check [Chapter 5](#chapter-5-the-app-contains-code-that-has-never-been-published) and [the section on what that code does](#what-the-unpublished-code-actually-does), and step 4 checks the citations behind [Chapter 7](#chapter-7-this-is-a-written-policy-not-an-oversight) and [Chapter 8](#chapter-8-october-2025-when-the-stated-reason-collided-with-reality). What these steps do **not** cover is stated at the end.

**1. The commit history**

```bash
curl -s https://gitlab.com/api/v4/projects/4142452/repository/commits | jq -r '.[] | "\(.created_at[0:10])  \(.title)"'
```

Expect three commits, nothing after 2019, no tags.

**2. The binary**

```bash
sha256sum org.telegram.plus.apk
# d332a1304fc0c0c3daecc8fe7321893f7a6e88ffb59916743d175bf626fbbfef

apksigner verify --print-certs org.telegram.plus.apk
# V3 cert SHA-256 6ebb622268aad319dbe8a1f414837d2843a9b35856aefb7dee2971a3d493f276
```

**3. The unpublished layer**

```bash
jadx --no-res --no-debug-info -d out org.telegram.plus.apk
ls out/sources/org/telegram/plus/          # 39 files, none of them published
grep -rn "test_ids" out/sources/org/telegram/plus/helpers/FirebaseHelper.java
grep -rn "isLoginCode" out/sources/org/telegram/messenger/PushListenerController.java
```

Then request the same path from the published tree:

```bash
curl -o /dev/null -w '%{http_code}\n' \
  https://gitlab.com/rafalense/plus-messenger/-/raw/master/TMessagesProj/src/main/java/org/telegram/plus/ads/AdsController.java
# 404
```

**4. The citations.** Open any `t.me/<channel>/<id>` link in this document. Every date given is that message's own timestamp, visible in any Telegram client.

**5. The moderation record.** The two GitLab issues and the GitHub issue linked in Chapter 14. Every quote is on the page.

---

# Chapter 13: What happened when this was reported

You now have the technical case, the ten-year record, and the outcome of every attempt to resolve it. This is what the surrounding open-source community did with it.

In roughly twelve hours: an account deleted before its post cleared moderation, two closed issues, a closed forum thread with its citations removed, and a written promise to keep watching the reporter.

**Not one person, on any platform, quoted a line of the evidence and said it was wrong.**

---

# Chapter 14: Wall of shame

Everyone below is a public account acting in a public capacity, and every quotation is verbatim from a page you can open. No motive is imputed to anyone, and none needs to be: in each case their own stated reasoning is the most damaging thing available, and I have simply left it where they put it.

---

## 14.1 vdbhb59 (`@flossboxin`)

His F-Droid forum profile carries the title **"Contributor, F-Droid Board Member"**, which I re-checked live on 2026-09-02 straight from [the forum's own JSON](https://forum.f-droid.org/u/vdbhb59.json) so that nobody has to take my word for it. He also holds **Developer** access on the [`fdroid/admin`](https://gitlab.com/fdroid/admin/-/issues/700) tracker, and on [GitLab](https://gitlab.com/flossboxin) and [GitHub](https://github.com/vdbhb59) he is easy enough to find. In the Telegram-FOSS repository, where the rest of this story happens, he holds no role at all.

At **03:47 UTC** the F-Droid forum account that filed this report was deleted. The email cited no rule, gave no warning and offered no appeal, saying only that the account *"has been deleted by a staff member."* The post itself had never been visible to a single human being; it was still sitting in the new-user moderation queue.

Two minutes later, at **03:49:43**, he turned up under the same report on [a different project's GitHub tracker](https://github.com/Telegram-FOSS-Team/Telegram-FOSS/issues/377#issuecomment-5504070601):

> *"please delete this comment from **the bot above**. The bot has come and posted on several forums. Just created account and posted this. **Banned them. Reporting this as well.**"*

Seven hours later, on F-Droid's own tracker, he explained himself at length:

> *"**I deleted your account, as I saw you as BOT**, which created an account and pasted some links (**including few dubious looking links**) to continue a 6 year old thread... Clickbait."*
>
> *"You shared links to a stale stuff, and **people may click on them out of cusriousity**. Moreover, what you were posting is **old data which people are already aware of**."*
>
> *"**You will remain banned and I will make sure to watch you in other places.**"*

Four reasons, and they fall over in the order given. The *dubious links* were two in number, because Discourse caps new accounts at two, and they went to `gitlab.com` and `github.com`, which are the two repositories the report is about. Asked to name the dubious one, he named nothing. For the record, every link this record has ever posted anywhere resolves to eight domains: `t.me`, `gitlab.com`, `github.com`, `play.google.com`, `appgallery.huawei.com`, `f-droid.org`, `plusmessenger.org` and `xdaforums.com`. No shortener, no redirect, not one.

The people who *may click out of curiosity* could not, because the topic never left the moderation queue. He is describing a danger to users from a post that no user was able to see, which is true only because he deleted it before any of them could.

The *old data which people are already aware of* was a SHA-256 computed the previous afternoon. Twenty-seven hours, from hash to deletion.

And the *6 year old thread* was a GitHub comment on another project, not the forum topic he deleted. This matters mainly because his colleague spent the following morning defending the same deletion on the opposite grounds, namely that the **new** forum post was off-topic. Two staff, two explanations that cannot both be true, neither withdrawn.

Now set that against F-Droid's own inclusion policy, which says the project *"compiles applications from publicly accessible source code to **verify that distributed binaries match their source code**."* That is, word for word, the thing this report documents a failure of. Their Code of Conduct asks members to *"assume good faith"* and reserves bans for *"serious or persistent offenders."* Their forum guidelines prohibit *"Responding to a post's tone instead of its actual content."*

Across everything he wrote about this report, the word *bot* appears repeatedly and the word *source* does not appear once. He never engaged the claim. He assessed the account.

So: a board member of a project whose entire reason for existing is checking that binaries match their published source deleted a report about a binary that does not match its published source, on the grounds that it was submitted by somebody new. Two minutes to decide, seven hours to justify, zero seconds on the evidence itself.

He then closed with *"I will make sure to watch you in other places"*, in writing, on a public tracker, under his own handle, seemingly under the impression that this was the strong finish.

---

## 14.2 Licaon_Kter

A long-standing F-Droid contributor with issue-closing rights on [`fdroid/admin`](https://gitlab.com/licaon-kter), which is the tracker F-Droid's Code of Conduct nominates for exactly this kind of complaint. So that is where the deletion went, as [issue 700](https://gitlab.com/fdroid/admin/-/issues/700), at 08:13 UTC.

He asked which app in F-Droid this concerned. At **09:03:10** he was told: none, and the reason it is in none is that [rafalense submitted it to F-Droid himself in March 2015, as "GNU GPL v2"](https://f-droid.org/forums/topic/plus/), where it was declined over bundled Play Services.

At **09:04:30**, eighty seconds later, he closed the issue:

> *"ah, ok then"*

Eighty seconds. Then, having closed it, he came back three minutes afterwards to add:

> *"if your very own FIRST post is an offtopic, sorry... but **I would have deleted your post and account too**"*
>
> *"you even admit knowing that what you did was not proper"*

The 2015 submission is the single fact that makes "off-topic" untenable, and it went unaddressed then and since.

A separate Code of Conduct report about the board member's conduct was opened at 09:14:37 as [issue 701](https://gitlab.com/fdroid/admin/-/issues/701). At 09:27 he closed that one too, as a *"duplicate of #700"*, without a single comment. One issue was about an account being deleted; the other was about a colleague of his pursuing the reporter onto another project's tracker. Filing those as duplicates of each other is a choice, and the person making it was the closest available colleague of the person named in the second one.

He then wrote, on the issue he had closed:

> *"this issue is not locked, no need for other issues, but you can continue to not assume good faith in my posts and **we can take other measures, if you insist**"*
>
> *"the reasoning was simple **'not related to F-Droid, we don't care'**, if you fail to grasp that, there's nothing more to discuss"*

*We don't care* would be a perfectly coherent position, and I would have accepted it, except that somebody wearing an F-Droid title had cared enough two hours earlier to open a stranger's issue on a different project and ask for the same report to be deleted there as well. In one morning the organisation managed to be both too uninterested to read the thing and sufficiently interested to chase it across platforms.

Eighty seconds is enough time to type *"ah, ok then"*. It is not enough time to open an eleven-year-old forum thread, read it, and revise a position based on it, and the three minutes he spent afterwards were spent defending the position rather than checking it.

The sequence, then. He closed the complaint about the deletion in eighty seconds. He closed the complaint about the man who made the deletion as a duplicate of the complaint about the deletion. He explained that F-Droid did not care. And then, in the same thread, he helpfully supplied that man's GitLab handle, thereby caring.

---

## 14.3 Oswald Boelcke, XDA Senior Moderator

Some credit is due elsewhere first. The original thread went in the wrong subforum and was closed for that reason by Senior Moderator **TNSMANI**, who then answered a direct question about where it should live:

> *"The thread looks ok at General Topics."*

That was at 10:39. The replacement went up in General Topics, which is the room a Senior Moderator had just pointed at. At **16:54**, [Oswald Boelcke](https://xdaforums.com/m/oswald-boelcke.7408621/) closed it:

> *"This thread is obviously **a rant about something that occurred or still occurs outside of XDA Forums**. As we don't control anything that happens outside of our website, we don't accept that such rants or fights are posted on our Forums."*

and, in the same breath:

> *"I've edited your OP and removed the **really extreme number of references to Telegram**."*

The really extreme number was about thirty, and they were `t.me/<group>/<id>` links. Not channels he runs, not invitations, not promotion of anything. Each one was the primary source for a specific quoted claim: the pinned rule, the admin enforcing it, the ads announcement, the users who paid and still saw ads. Footnotes, in other words. Every one of them now reads:

```
{Mod edit: References to Telegram removed!}
```

XDA's rule against Telegram links is real and predates all of this, and it exists to stop people advertising their chat groups. Applying it to citations is a decision rather than an obligation, and so is looking at a post consisting of a licence quotation, a commit log, a SHA-256 table and a dex inventory and calling it *obviously a rant*.

The damage here is the worst in this chapter, and it is not to anyone's feelings. That thread URL had already gone out in writing, to licence enforcement organisations and to press, as the place where the evidence and its sources could be found. Those people now arrive at a public page that appears to make thirty assertions and support none of them, which is exactly true, and true only because the support was deleted after they were sent the link.

Two Senior Moderators reached opposite conclusions about the same thread inside seven hours, and the cost fell entirely on the person who had asked permission first and then done as he was told.

The rule he enforced exists to stop people advertising their Telegram groups on XDA. What it actually removed, on this occasion, was the evidence that a developer has not published his source code in nine years. The rule worked exactly as written.

He deleted thirty citations from a post and closed it in the same action for being unsupported. By the time he clicked the second button, he was right.

---

## 14.4 F-Droid forum staff

There is nobody to name here, which is the entry.

F-Droid does not publish its staff or moderator list. [`forum.f-droid.org/about.json`](https://forum.f-droid.org/about.json) returns empty arrays where the names would be. The account was deleted at 03:47 by "a staff member", no rule was cited, the topic never left moderation, and no appeal route was offered.

An organisation that deletes accounts without citing a rule, and separately declines to publish who its moderators are, has closed both routes to accountability in a single stroke. You cannot appeal the reason, because none was given. You cannot ask the person, because there is no list. It is an admirably efficient arrangement and I assume nobody designed it on purpose.

Both questions went onto F-Droid's own tracker regardless. One was eventually answered, seven hours later, by the man volunteering that he had done it. The rule has never been named, and at this point it seems fair to conclude there wasn't one.

---

## 14.5 The pattern

Everything above happened between 03:47 and 14:54 UTC on 2 September 2026. The forum account was deleted before its post cleared moderation, and two minutes later a board member was on another project's tracker calling the report bot output. The complaint about that deletion was closed eighty seconds after it was answered, and the conduct report naming him was closed as a duplicate by the same person who had closed the first. That afternoon a forum moderator stripped the citations out of the remaining public copy and closed the thread.

Each of those was somebody applying a rule they were entitled to apply, and no coordination between them is alleged or evidenced. Spam heuristics, off-topic rules, duplicate triage, a jurisdiction rule. Individually defensible, every one.

What none of them did was engage with the evidence. Across four venues and a full working day, nobody quoted a hash, a commit, a date or a line of the licence and said it was wrong. Nobody has since. The one party with an actual obligation here was left entirely undisturbed throughout, and continues to be.

---

# Chapter 15: What remains unresolved

As of the compilation date:

1. **The current release still ships unpublished code.** 12.10.1.0, on Google Play, 50M+ installs.
2. **No source has been published.** The newest remains 4.2.1.1, September 2017.
3. **No written offer exists.** Not in the app, on Play, on the site, or in either repository.
4. **The developer has not responded.** [Issue 84](https://gitlab.com/rafalense/plus-messenger/-/issues/84) has no reply, alongside issues 20 and 22 from 2018.
5. **The AppGallery listing still discloses no monetisation.**
6. **The F-Droid ban stands**, the rule broken still unnamed.
7. **The XDA thread remains closed**, its citations still deleted.

---

# Chapter 16: Requested remediation

After all of the above, here is the entire remedy. Either item closes the matter completely, permanently, with no further argument from anyone including me:

### Option A: publish (GPLv2 §3a)

1. Push the current tree to https://gitlab.com/rafalense/plus-messenger.
2. Include `org/telegram/plus`, the whole package, ads and billing included.
3. Include the build scripts.

### Option B: offer (GPLv2 §3b)

1. Write one paragraph offering the corresponding source to any third party, valid three years.
2. Put it in the Play listing and in the app's About screen.

Option A is the obligation as the licence describes it. Option B is a standing commitment: an offer valid for three years carries a duty to actually supply the source on request for that period, which is a real undertaking rather than a formality.

**[inference]** Until one of them happens, on my reading of section 4 the licence has terminated and distribution continues without one. That is the only interpretive legal claim in this document, no court has ruled on it, and it is flagged rather than left for a hostile reader to find.

---

# Chapter 17: Conclusion

The case rests on a small number of facts, every one of them checkable in minutes.

The newest source ever published for Plus Messenger is from September 2017. The version distributed today is from August 2026. The binary contains current upstream Telegram code, which is GPL-licensed, alongside roughly 11,400 lines under `org.telegram.plus` that appear in no repository at any version. That unpublished portion is the advertising, analytics and billing layer, and it is the part that takes money from users. No written offer for the source exists on any distribution channel. Requests have been made continuously since 2016, and the support group's pinned rules declare the question off-topic and explain that the source is withheld to stop other developers adding advertising. In October 2025 the developer added advertising.

Those facts establish a distribution practice that section 3 does not permit. They are claims about conduct and artifacts, which is why they can be verified, and why the conclusion holds regardless of what anyone believes about the developer's intentions.

One consequence outlives the licence argument. The section on the unpublished code describes a mechanism inside the shipped binary that reads login codes out of a user's Telegram message history and uploads them, gated behind a check against two hardcoded phone numbers. It is almost certainly a developer test harness, and the document says so. Nobody can demonstrate that, because nobody can read the code. The ships-to-everyone half is verifiable. The only-fires-for-two-people half rests on a decompiled `if` statement and the goodwill of one person.

That is what nine years of withheld source actually costs, and it is not a paperwork cost. Fifty million downloads of a messaging client, carrying an unauditable payload, in an ecosystem whose entire safety model assumes somebody can check. Nekogram was caught because its source could be diffed against its binary. Here there has been nothing to diff since 2017.

Two things would end this, both listed in Chapter 16, neither of them onerous. Until one happens, the position stands: the corresponding source has not been published, the users have no way to verify what they are running, and the obligation attached to the code the app was built on has gone unmet for nine years while the app earned money.

Nobody has yet identified a part of that which is wrong.

---

# A word to anyone deciding whether to install this, or anything like it

**This is not an accusation that Plus Messenger contains malware.** Nothing in this document supports that claim, and the unpublished-code section says plainly that the one sensitive mechanism found in the binary is gated to two of the developer's own test numbers. Read that section and draw your own conclusion. It is about trust, and about what you are able to check.

Think carefully before installing any third-party app, and think harder when its developer has repeatedly failed to honour the licence of the code it is built on.

Open source is not valuable because the word "open" appears in a store listing. It is valuable because of a specific chain of things you are able to do:

1. **Read** what the program actually does.
2. **Compare** the published source against the binary you were shipped.
3. **See what changed** between one release and the next.
4. **Verify** that the thing running on your phone is the thing the source describes.

The corresponding-source requirement in GPLv2 section 3 is what keeps that chain intact. It is not paperwork, and it is not about credit. It is the mechanism.

When a developer withholds the source for the version he ships, that chain breaks at the first link, and every link after it. You are no longer running software you can verify. You are running software you have decided to trust, which is a different thing, and the decision is being made with less information than the licence was written to give you.

Notice how little of this depends on anyone's intentions. A developer can be entirely honest and still leave you unable to check. That is precisely why the obligation is unconditional in the licence text: it does not ask whether you meant well.

So the reasoning here is not "he broke the licence, therefore the app is dangerous." It is narrower and more durable:

> A repeated, documented, decade-long refusal to publish corresponding source is not evidence of malicious software. It **is** a legitimate reason to apply a much higher standard of scrutiny before trusting that software with your device, your accounts, your messages, your files and your personal data.

Ask what you are actually granting. A messaging client sees your conversations, your contacts, your phone number, your login codes and your files. It runs with those permissions every day, in the background, on the device you carry. That is a large amount of trust to extend to a binary that nobody outside one person has ever been able to audit, and that has been unauditable since 2017.

The Nekogram case above is the cleanest illustration available. That fork was caught because it published source somebody could diff against the shipped APK. The check worked. It worked because the material to run the check existed.

Here there is nothing to diff. There has been nothing to diff for nine years, and the only reason anything in the unpublished-code section is documented at all is that one person spent an evening running a decompiler, which is slow, incomplete, and something virtually nobody does before installing an app.

None of this requires you to uninstall anything. It asks you to notice what you gave up, and to hold the developer to the one condition attached to the code he built on. If he publishes the source, every argument in this document evaporates, and you get the safeguard back. That remains available to him today.

---

## Notice

**Nature of this document.** A compliance record compiled by a recipient of the binary, exercising the right that GPLv2 section 3 gives every recipient. The author is not a lawyer and this is not legal advice. The single interpretive legal claim, that section 4 has terminated the licence, appears in Chapter 17 and is flagged there.

**Rights holders.** Only the upstream copyright holders can bring an action or compel a store removal. They were notified on 2026-09-01, before any part of this record was published, and nothing here is filed on their behalf or with their authority.

**Disputed facts.** Anyone named here who disputes a quotation, a date, a hash or a characterisation should [open an issue](../../issues), and it will be corrected or removed.

**Contact.** Direct anything arising from this record to [issue 84](https://gitlab.com/rafalense/plus-messenger/-/issues/84) or to this repository's issues. The remedy the licence asks for is source code, and it is obtainable from one person. Approaching anyone named in Chapter 14 undermines the record and helps nobody.

**Scope.** Each action in Chapter 14 is attributed to the account that took it, on the evidence of that account's own public words.

Compiled 2026-09-01 and 2026-09-02.
