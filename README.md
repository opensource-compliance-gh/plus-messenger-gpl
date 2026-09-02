# Fifty million downloads of code nobody outside one person has been allowed to read

**The app:** Plus Messenger (`org.telegram.plus`), 50,000,000+ Google Play installs, a fork of Telegram for Android.
**The licence:** GPL-2.0-or-later. It permits the fork. It attaches one condition to distributing the binary: supply the corresponding source, or a written offer to supply it.
**The problem:** the newest source ever published is from **13 September 2017**. The version on Google Play today is from **29 August 2026**.

On its own that's just a stale repository. Here's why it isn't:

The binary distributed as version 12.10.1.0 contains an advertising engine, an analytics pipeline and a Google Play Billing integration, under the package `org.telegram.plus`, that **has never appeared in any published source, at any version, in eleven years**. That code sells ad removal for **EUR 5.99 to 99.99**. There is no written offer for the source anywhere: not in the app, not on Play, not on the official site, not in either repository.

Every claim in this document is backed by something you can open in a browser or recompute on your own machine in about ten minutes. The exact APK is identified by SHA-256. The signing certificate is included, so the "that's a third-party repack" defence is closed before it can be raised. Chapter 12 is a copy-pasteable verification script.

None of this is new. It has been raised in the developer's own support groups since **2016**, where a pinned rule declares the question off-topic and an admin tells people to read the rules again.

---

**Reading order.** The technical case is Chapters 3 to 9. If you want to check the work rather than read it, skip to [Chapter 12: Verify all of it yourself](#chapter-12-verify-all-of-it-yourself). The account of what happened when this was reported is Chapters 13 and 14, placed after the technical case because it is not the point.

---

## Index

- **[Chapter 1: How Plus got here](#chapter-1-how-plus-got-here)**
- **[Chapter 2: What the licence actually requires](#chapter-2-what-the-licence-actually-requires)**
- **[Chapter 3, Finding 1: the published source stopped in 2017](#chapter-3-finding-1-the-published-source-stopped-in-2017)**
- **[Chapter 4, Finding 2: the changelog says the source is being updated](#chapter-4-finding-2-the-changelog-says-the-source-is-being-updated)**
- **[Chapter 5, Finding 3: the app contains code that has never been published](#chapter-5-finding-3-the-app-contains-code-that-has-never-been-published)**
    - [Finding 3b: what the unpublished code actually does](#finding-3b-what-the-unpublished-code-actually-does)
- **[Chapter 6, Finding 4: there is no written offer either](#chapter-6-finding-4-there-is-no-written-offer-either)**
- **[Chapter 7, Finding 5: this is a written policy, not an oversight](#chapter-7-finding-5-this-is-a-written-policy-not-an-oversight)**
- **[Chapter 8, Finding 6: October 2025, when the stated reason collided with reality](#chapter-8-finding-6-october-2025-when-the-stated-reason-collided-with-reality)**
- **[Chapter 9, Finding 7: the same app, a different store, a different story](#chapter-9-finding-7-the-same-app-a-different-store-a-different-story)**
- **[Chapter 10: What was done about it](#chapter-10-what-was-done-about-it)**
- **[Chapter 11: Testing the defences](#chapter-11-testing-the-defences)**
- **[Chapter 12: Verify all of it yourself](#chapter-12-verify-all-of-it-yourself)**
- **[Chapter 13: What happened when this was reported](#chapter-13-what-happened-when-this-was-reported)**
- **[Chapter 14: Wall of shame](#chapter-14-wall-of-shame)**
    - [14.1 vdbhb59 (`@flossboxin`)](#141-vdbhb59-flossboxin)
    - [14.2 Licaon_Kter](#142-licaon_kter)
    - [14.3 Oswald Boelcke, XDA Senior Moderator](#143-oswald-boelcke-xda-senior-moderator)
    - [14.4 F-Droid forum staff, collectively](#144-f-droid-forum-staff-collectively)
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

## Summary of findings

| # | Finding | Where |
|---|---|---|
| **F1** | No corresponding source has been published for any release since 2017-09-13 | Chapter 3 |
| **F2** | Release notes state "Source code updated to vX" against a repository with zero code commits since 2017 | Chapter 4 |
| **F3** | The distributed binary contains an ad, analytics and billing layer (`org.telegram.plus`) absent from every published source tree | Chapter 5 |
| **F3b** | The unpublished layer is 11,440 lines including a Firebase Auth/Firestore backend and a push-triggered login-code retrieval path gated to two hardcoded numbers | Chapter 5 |
| **F4** | No section 3(b) written offer exists in the app, on any store listing, or on the official site | Chapter 6 |
| **F5** | Withholding the source is stated policy, pinned publicly since 2019-06-17, and enforced by group administrators | Chapter 7 |
| **F6** | The stated justification for withholding (preventing others from adding advertising) was contradicted by the distributor's own conduct on 2025-10-02 | Chapter 8 |
| **F7** | Monetisation is disclosed on Google Play and undisclosed on Huawei AppGallery, contrary to Telegram API ToS §3.2 | Chapter 9 |

## Standard applied

1. A statement of fact is accompanied by a URL you can open or an artifact you can recompute. It is not asserted otherwise.
2. Reasoning that goes beyond the primary evidence is marked **[inference]**.
3. Personal judgement is marked **[opinion]**.
3a. Applying licence text to facts is analysis, not fact. Chapters 2, 4, 6 and 16 contain legal reasoning. None of it is a court ruling and none of it should be read as one.
4. Where a defence exists, it is stated in its strongest form and then tested against the evidence. Chapter 11 does this for ten of them.
5. Quotations are verbatim, with the date and the source of each. Translations are given alongside the original, never in place of it.
6. Claims that could not be substantiated were excluded. Two are named in the Notice at the end.

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

# Chapter 3, Finding 1: the published source stopped in 2017

### What I found

His own group rules point users to the GitLab repository as the current one. It has three commits, and only one of them contains code.

### Evidence

**1. The complete commit history.** Not a selection. All of it.

```
0978c068   2017-09-13   Add readme.md
1d961518   2017-09-13   Update to v4.2.1.1        <-- last commit containing code, ever
b418c867   2019-02-07   Update README.md          <-- documentation only
```

Fetch it yourself with no account:

```
https://gitlab.com/api/v4/projects/4142452/repository/commits
```

**2. No tags.** The project has never tagged a release.

**3. The version in the tree.** `build.gradle` carries `versionCode 1047`, the 4.2.1.1 era, September 2017.

**4. The GitHub repository is not a fallback.** It is older still: **v2.5.2.1, last code commit 2015-03-11.**

**5. Two people already filed the obvious issue and were ignored.** Both cite the licence. Both have been open since **October 2018** with no reply:
   - https://gitlab.com/rafalense/plus-messenger/-/issues/20
   - https://gitlab.com/rafalense/plus-messenger/-/issues/22

### Why it matters

| | Version | Date |
|---|---|---|
| Newest source ever published | **4.2.1.1** | 2017-09-13 |
| Currently shipping on Google Play | **12.10.1.0** | 2026-08-29 |

That is eight major versions across nine years, and section 3 requires source corresponding to the binary being distributed. There is none for anything released since 2017.

### What this establishes

No corresponding source has been published for any release in nine years. Nothing more yet: at this stage, a solo developer with a stale repository is still a plausible reading.

It survives about another ten minutes. [Chapter 4](#chapter-4-finding-2-the-changelog-says-the-source-is-being-updated) is what breaks it, and the strongest counter-argument available here, that the published source may correspond to an archived 2017 build, is tested in [Chapter 11](#chapter-11-testing-the-defences).

---

# Chapter 4, Finding 2: the changelog says the source is being updated

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

# Chapter 5, Finding 3: the app contains code that has never been published

Everything so far concerns what is *missing*. This is what is *shipped*, and it is where the case stops being about tidiness. Measure it against the four words in [Chapter 2](#chapter-2-what-the-licence-actually-requires): this chapter establishes what "corresponding" has to cover, [Chapter 6](#chapter-6-finding-4-there-is-no-written-offer-either) shows that the alternative route of a written offer was not taken either, and [Finding 3b](#finding-3b-what-the-unpublished-code-actually-does) examines what the unpublished code does once it is running.

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

**[correction, 2026-09-02]** An earlier draft said "he built it and he signed it". That overstated what a signature proves under Play App Signing, and has been narrowed.

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

## Finding 3b: what the unpublished code actually does

Everything above establishes that the code exists and was never published. This section is about what is in it, and it is the point where the licence stops being a formality. It is the basis for the warning at the end of this document, and for the argument in [Chapter 17](#chapter-17-conclusion) that the cost of withheld source is measured in what nobody can check.

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

One small illustration of what unreviewed code looks like. The push login handler guards itself with:

```java
if (str2 == null && !str2.equals("-1"))
```

A null check followed by a method call on the same reference, in the same condition. It can never be true, and if it ever were it would throw immediately. Dead code, shipped to fifty million devices, in the security-sensitive path. No reviewer has ever seen it, because no reviewer has ever been allowed to.

### Why this is not a hypothetical concern

Five months before this record was compiled, a different Telegram fork demonstrated exactly the risk being described.

On 2026-04-03 it was [reported on r/Android](https://www.reddit.com/r/Android/comments/1sb3h81/nekogram_caught_collecting_user_account/) that **Nekogram** was sending users' phone numbers and usernames to a developer-controlled Telegram bot, via, in the reporter's words:

> "obfuscated injected code **that is not in the source code provided on GitHub**. The packaged APK with the malicious code is distributed via Play Store, GitHub Releases and their Telegram channel."

The report states the developer acknowledged it. A related technical discussion is at [net4people/bbs issue 601](https://github.com/net4people/bbs/issues/601). Readers should evaluate that case on its own evidence; it is cited here for one narrow point, not as a finding of this document.

**The narrow point.** Nekogram publishes source. That is *why* somebody could compare the published source against the shipped APK, find the difference, and raise it. The discovery mechanism was a diff.

Plus Messenger cannot be checked that way. There is no current source to diff against, and has not been since 2017. The only reason the material in Finding 3b is documented here at all is that it was decompiled by hand from a binary, which is slow, lossy, and something almost nobody does.

**To be explicit, because the distinction matters:** nothing in this document alleges that Plus Messenger does what Nekogram was reported to have done. The login-code path described above is gated to two hardcoded numbers, and for every other account it does nothing. The comparison is about *auditability*, not about conduct.

That is the answer to anyone who regards a nine-year source gap as a paperwork problem. In the same ecosystem, in the same year, in an app of the same type, the published-source requirement is what surfaced a real privacy incident. The app that published source got audited. The app that never published source, with fifty million installs, has never been audited by anyone, and would not be now if somebody had not spent an evening running `jadx`.


---

# Chapter 6, Finding 4: there is no written offer either

### What I found

Section 3 offers an alternative to shipping a source tarball with every download: a written offer to supply it on request, quoted in full in [Chapter 2](#chapter-2-what-the-licence-actually-requires). It was not used either. What using it would involve is set out in [Chapter 16](#chapter-16-requested-remediation).

### Evidence

The decoded app resources were searched for "GNU General Public License", for "source code", and for repository URLs. The complete set of results:

1. A theme-preview joke string.
2. An error message about waiting for Telegram to update its source code.

First-party screenshots of the running app confirm that Settings terminates at a version number, and the Help section contains no licence or source entry. The Play listing carries no source link. `plusmessenger.org` carries no source link.

### What this establishes

There is no section 3(a) compliance (no corresponding source) and no section 3(b) compliance (no written offer). Both routes the licence provides are unused.

Those two strings are the entire licence footprint of an application built on GPL code and installed fifty million times.

---

# Chapter 7, Finding 5: this is a written policy, not an oversight

One stale repository is an accident. This is the chapter where that reading stops working, and the rule quoted below is what [Chapter 8](#chapter-8-finding-6-october-2025-when-the-stated-reason-collided-with-reality) then measures the developer's own conduct against.

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

# Chapter 8, Finding 6: October 2025, when the stated reason collided with reality

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

# Chapter 9, Finding 7: the same app, a different store, a different story

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

Nothing here asks for trust. Roughly ten minutes, start to finish. Step 1 checks [Finding 1](#chapter-3-finding-1-the-published-source-stopped-in-2017), steps 2 and 3 check [Finding 3](#chapter-5-finding-3-the-app-contains-code-that-has-never-been-published) and [Finding 3b](#finding-3b-what-the-unpublished-code-actually-does), and step 4 checks the citations behind [Finding 5](#chapter-7-finding-5-this-is-a-written-policy-not-an-oversight) and [Finding 6](#chapter-8-finding-6-october-2025-when-the-stated-reason-collided-with-reality). What these steps do **not** cover is stated at the end.

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

Everyone named below is a public account acting in a public capacity. Every quote is verbatim from a public page. No motive is imputed to anybody, because none can be proven and none is needed. Any of them who disputes a quote or a timestamp will have it corrected.

---

## 14.1 vdbhb59 (`@flossboxin`)

**Role.** F-Droid forum profile title: **"Contributor, F-Droid Board Member"**, re-verified live on 2026-09-02 via the forum's own JSON endpoint. Holds **Developer** access on the `fdroid/admin` GitLab tracker. No public role was found in the Telegram-FOSS repository.

Accounts, so the role claims above can be checked rather than taken on trust:

1. F-Droid forum: [forum.f-droid.org/u/vdbhb59](https://forum.f-droid.org/u/vdbhb59) ([JSON](https://forum.f-droid.org/u/vdbhb59.json), where the title string appears)
2. GitLab, as `@flossboxin`: [gitlab.com/flossboxin](https://gitlab.com/flossboxin) — the handle supplied by his colleague on issue 700
3. GitHub: [github.com/vdbhb59](https://github.com/vdbhb59), account created 2020-02-06

**What he did.** At **03:47 UTC** on 2026-09-02, the F-Droid forum account that submitted this report was deleted. The notification email gave one reason: the account *"has been deleted by a staff member."* No rule cited, no warning, no appeal. The topic was still in the new-user moderation queue and had never been visible to anybody.

At **03:49:43 UTC**, two minutes later, he appeared under the record comment on a **different project's** GitHub tracker:

> *"please delete this comment from **the bot above**. The bot has come and posted on several forums. Just created account and posted this. **Banned them. Reporting this as well.**"*

**Evidence.**

1. [Telegram-FOSS issue 377, comment 5504070601](https://github.com/Telegram-FOSS-Team/Telegram-FOSS/issues/377#issuecomment-5504070601): the comment above, timestamped.
2. [fdroid/admin issue 700, note 3774853608](https://gitlab.com/fdroid/admin/-/issues/700): his own explanation, seven hours later, quoted below.

At 10:56 UTC he explained the reasoning:

> *"**I deleted your account, as I saw you as BOT**, which created an account and pasted some links (**including few dubious looking links**) to continue a 6 year old thread... Clickbait."*
>
> *"You shared links to a stale stuff, and **people may click on them out of cusriousity**. Moreover, what you were posting is **old data which people are already aware of**."*
>
> *"**You will remain banned and I will make sure to watch you in other places.**"*

**Why the reasoning fails.** Four claims, all checkable, none surviving.

| His claim | The record |
|---|---|
| *"dubious looking links"* | The deleted post contained exactly **two** links, because Discourse caps new accounts at two: `gitlab.com` and `github.com`. Across the entire public record every link resolves to eight domains: `t.me` (29), `gitlab.com` (10), `github.com` (5), plus one each of `play.google.com`, `appgallery.huawei.com`, `f-droid.org`, `plusmessenger.org`, `xdaforums.com`. No shortener, no redirect. He was asked to name the dubious one. He did not. |
| *"people may click on them out of cusriousity"* | The topic never left the moderation queue. Nobody could click anything. He is describing a hazard to users from a post no user could see, which he deleted before any user could see it. |
| *"old data which people are already aware of"* | Ads announced 2025-10-02. APK dated 2026-08-29. Hashed 2026-09-01. Deleted 2026-09-02. The data was 27 hours old. |
| *"to continue a 6 year old thread"* | Describes a GitHub comment, not the forum topic. It also contradicts his own colleague, whose entire defence was that the **first forum post** was off-topic. Two staff, two mutually exclusive reasons for one deletion, neither withdrawn. |

**Damage caused.** The report was removed from the one venue whose stated mission is verifying that distributed binaries match their published source, before a single member could read it, and then pursued to a second project's tracker for deletion there too. The ban stands.

**The contradiction.** F-Droid's own inclusion policy: the project *"compiles applications from publicly accessible source code to **verify that distributed binaries match their source code**."* Their Code of Conduct: *"assume good faith"*, bans reserved for *"serious or persistent offenders"*. Their forum guidelines specifically prohibit *"Responding to a post's tone instead of its actual content."*

He deleted a report about a binary that does not match its published source, on the grounds that the author's account was new.

**Closer.** He gave four reasons across seven hours. The links were two, both to the repositories under discussion. The clicking risk applied to a post nobody could see. The stale data was a hash taken the previous day. And the six-year-old thread he described was on a different site. A board member of a project whose stated purpose is checking binaries against published source disposed of a binary-versus-source report in two minutes, and closed by putting "I will make sure to watch you in other places" in writing, on a public tracker, under his own handle.

---

## 14.2 Licaon_Kter

**Role.** Long-standing F-Droid contributor with issue-closing rights on `fdroid/admin`, the tracker F-Droid's own Code of Conduct designates for complaints.

Accounts:

1. GitLab: [gitlab.com/licaon-kter](https://gitlab.com/licaon-kter)
2. F-Droid forum: [forum.f-droid.org/u/Licaon_Kter](https://forum.f-droid.org/u/Licaon_Kter)

**What he did.** The deletion was reported there as issue 700 at 08:13 UTC. He asked which app in F-Droid this concerned.

At **09:03:10Z** he was answered: it is not in F-Droid, and the reason it is not is that **rafalense submitted it to F-Droid himself on 2015-03-27 as "GNU GPL v2"**, declined for bundling Play Services.

At **09:04:30Z**, eighty seconds later, he closed the issue:

> *"ah, ok then"*

At 09:07:52Z, having already closed it:

> *"if your very own FIRST post is an offtopic, sorry... but **I would have deleted your post and account too**"*
>
> *"you even admit knowing that what you did was not proper"*

A separate Code of Conduct report about the board member's conduct was opened as issue 701 at 09:14:37Z. At 09:27 UTC **he closed that one too**, as a *"duplicate of #700"*, with zero comments. Then, on 700:

> *"this issue is not locked, no need for other issues, but you can continue to not assume good faith in my posts and **we can take other measures, if you insist**"*
>
> *"the reasoning was simple **'not related to F-Droid, we don't care'**, if you fail to grasp that, there's nothing more to discuss"*

In the same thread he supplied vdbhb59's GitLab handle, `@flossboxin`, while maintaining that the complaint about vdbhb59 was not F-Droid related.

**Evidence.**

1. [fdroid/admin issue 700](https://gitlab.com/fdroid/admin/-/issues/700): the deletion complaint, closed in 80 seconds. All quotes above are in its note history.
2. [fdroid/admin issue 701](https://gitlab.com/fdroid/admin/-/issues/701): the Code of Conduct report, closed as a duplicate with no comment.
3. [f-droid.org/forums/topic/plus/](https://f-droid.org/forums/topic/plus/): the 2015 submission that makes "off-topic" untenable.

**Why the reasoning fails.** The reply that closed the issue came eighty seconds after the message containing the 2015 submission link. Whatever was or was not read in that interval, the "off-topic" characterisation went unrevised afterwards, and the developer's own 2015 submission of this app to F-Droid under the GPL is the one fact that bears directly on it.

Issue 700 was about an account deletion. Issue 701 was about a board member's conduct. Merging them as duplicates removed the only complaint naming a specific person, and it was merged by that person's colleague.

**Damage caused.** Both routes F-Droid's Code of Conduct provides for complaints were closed by the same individual, one in eighty seconds, the other without a single comment. Three questions were asked repeatedly. One was eventually answered, seven hours later and by the person responsible himself. The other two were not: which rule the account broke, and whether pursuing a reporter onto another project's tracker is acceptable conduct for someone holding an F-Droid title.

**The contradiction.** *"We don't care"* would be coherent if anyone had acted on it. Somebody holding an F-Droid title cared enough, two minutes after the deletion, to open a different project's tracker and ask for the same report to be deleted there. In one morning the organisation was simultaneously too uninterested to read the report and sufficiently interested to chase it across platforms.

**Closer.** He closed the complaint about the deletion in eighty seconds, closed the complaint about the person who made it as a duplicate of the first, wrote that F-Droid did not care, and in the same thread supplied that person's GitLab handle.

---

## 14.3 Oswald Boelcke, XDA Senior Moderator

**Role.** Senior Moderator, Moderator Committee, xdaforums.com: [xdaforums.com/m/oswald-boelcke.7408621](https://xdaforums.com/m/oswald-boelcke.7408621/)

**What happened first, to his colleague's credit.** The first thread (4800302) was posted in the wrong subforum and closed for that reason by Senior Moderator **TNSMANI**, correctly and courteously. The replacement's location was then queried in advance, and at **10:39** TNSMANI replied:

> *"The thread looks ok at General Topics."*

**What he did.** The replacement thread (4800334) was posted at 09:56 CEST in General Topics, which is where a Senior Moderator had just confirmed it belonged. At **16:54 CEST** he closed it:

> *"This thread is obviously **a rant about something that occurred or still occurs outside of XDA Forums**. As we don't control anything that happens outside of our website, we don't accept that such rants or fights are posted on our Forums."*

and, in the same post:

> *"I've edited your OP and removed the **really extreme number of references to Telegram**."*

**Evidence.**

1. [xdaforums.com/t/4800334/](https://xdaforums.com/t/4800334/): the closed thread. The opening post now displays `{Mod edit: References to Telegram removed!}` roughly thirty times, in place of its citations.
2. The moderator conversation in which the location was approved seven hours earlier, quoted above.

**Why the reasoning fails.** The "really extreme number of references" were roughly thirty `t.me/<group>/<id>` links. Not promotion, not invitations, not channels the poster owns or profits from. Each was the primary source for one specific quoted claim. They are footnotes.

XDA's rule against Telegram references is real, predates this case, and exists to stop people advertising their channels. Applying it to footnotes is a decision, not an obligation. So is describing a post consisting of a licence quotation, a commit log, a SHA-256 table and a dex inventory as *"obviously a rant."*

**Damage caused.** This is the most consequential entry in the chapter. That thread URL had already been given, in writing, to licence enforcement organisations and press contacts as the location where the evidence and its sources lived. Those citations now resolve to a public thread that appears to make thirty unsupported assertions, having been made to appear that way by the deletion of the support. A reader arriving today would reasonably conclude the author had no sources, and would be wrong because of a moderation action.

**The contradiction.** Two Senior Moderators reached opposite conclusions about the same thread within seven hours. The person who bore the cost is the one who asked permission first and did what he was told.

**Closer.** He edited roughly thirty evidentiary links out of the opening post and closed the thread in the same action. The rule he applied exists to stop people advertising their chat channels. What it removed was the sourcing of a licence analysis, and what remains on the page is a post that now reads as thirty unsupported assertions.

---

## 14.4 F-Droid forum staff, collectively

**Role.** Unknown. F-Droid's staff and moderator lists are not public: [`forum.f-droid.org/about.json`](https://forum.f-droid.org/about.json) returns empty lists. No individual appears in this entry for that reason, and the gap matters: an organisation that deletes accounts without citing a rule *and* does not publish who its moderators are has removed both halves of accountability at once.

**What happened.** Account deleted 03:47 UTC. No rule cited. Topic never released from moderation. No appeal route offered.

**Damage caused.** The venue whose entire purpose is verifying that binaries match their published source removed a report about a binary that does not match its published source, before publication, for reasons it has still not stated.

**Closer.** The deletion notice named no rule and no person. Both were asked for on F-Droid's own tracker, which is where their Code of Conduct sends complaints. The person was eventually named, by himself, seven hours later. The rule never was.

---

## 14.5 The pattern

Everything in this chapter happened between 03:47 and 14:54 UTC on 2 September 2026. The forum account was deleted before its post cleared moderation, and two minutes later a board member was on another project's tracker describing the report as bot output. The complaint about that deletion was closed eighty seconds after it was answered, and the conduct report naming him was closed as a duplicate by the same person who had closed the first one. That afternoon a forum moderator removed the citations from the remaining public copy and closed the thread.

Each of those was somebody applying a rule they were entitled to apply, and no coordination between them is alleged or evidenced. What none of them did was engage with the evidence. Across four venues and a full working day, no response quoted a hash, a commit, a date or a line of the licence and said it was wrong, and the distributor was left undisturbed throughout.

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

---

# Chapter 17: Conclusion

Strip out the moderation, the mockery and the narrative, and a short list of facts remains. They are the whole case, and each one is checkable in minutes.

The newest source ever published for Plus Messenger is from September 2017. The version distributed today is from August 2026. The binary contains current upstream Telegram code, which is GPL-licensed, alongside roughly 11,400 lines under `org.telegram.plus` that appear in no repository at any version. That unpublished portion is the advertising, analytics and billing layer, and it is the part that takes money from users. No written offer for the source exists on any distribution channel. Requests have been made continuously since 2016, and the support group's pinned rules declare the question off-topic and explain that the source is withheld to stop other developers adding advertising. In October 2025 the developer added advertising.

What that establishes is a distribution practice that section 3 does not permit. It does not establish anything about the developer's character, his intentions, or the safety of his software, and this document has been careful not to claim otherwise.

The part worth carrying away is narrower than the licence argument and outlives it. Finding 3b describes a mechanism inside the shipped binary that reads login codes out of a user's Telegram message history and uploads them, gated behind a check against two hardcoded phone numbers. It is almost certainly a developer test harness, and the document says so. Nobody can demonstrate that, because nobody can read the code. The ships-to-everyone half is verifiable. The only-fires-for-two-people half rests on a decompiled `if` statement and the goodwill of one person.

That is what nine years of withheld source actually costs, and it is not a paperwork cost. Fifty million downloads of a messaging client, carrying an unauditable payload, in an ecosystem whose entire safety model assumes somebody can check. Nekogram was caught because its source could be diffed against its binary. Here there has been nothing to diff since 2017.

Two things would end this, both listed in Chapter 16, neither of them onerous. Until one happens, the position stands: the corresponding source has not been published, the users have no way to verify what they are running, and the obligation attached to the code the app was built on has gone unmet for nine years while the app earned money.

If any part of that is wrong, it will be corrected. Nobody has yet identified a part that is.

---

# A word to anyone deciding whether to install this, or anything like it

**This is not an accusation that Plus Messenger contains malware.** Nothing in this document supports that claim, and Finding 3b says plainly that the one sensitive mechanism found in the binary is gated to two of the developer's own test numbers. Read that section and draw your own conclusion. It is about trust, and about what you are able to check.

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

The Nekogram case in Finding 3b is the cleanest illustration available. That fork was caught because it published source somebody could diff against the shipped APK. The check worked. It worked because the material to run the check existed.

Here there is nothing to diff. There has been nothing to diff for nine years, and the only reason anything in Finding 3b is documented at all is that one person spent an evening running a decompiler, which is slow, incomplete, and something virtually nobody does before installing an app.

None of this requires you to uninstall anything. It asks you to notice what you gave up, and to hold the developer to the one condition attached to the code he built on. If he publishes the source, every argument in this document evaporates, and you get the safeguard back. That remains available to him today.

---

## Notice

**Nature of this document.** A compliance record compiled by a recipient of the binary, exercising the right that GPLv2 section 3 gives every recipient. The author is not a lawyer and this is not legal advice. The single interpretive legal claim, that section 4 has terminated the licence, appears in Chapter 17 and is flagged there.

**Rights holders.** Only the upstream copyright holders can bring an action or compel a store removal. They were notified on 2026-09-01, before any part of this record was published, and nothing here is filed on their behalf or with their authority.

**Claims deliberately excluded.** Two allegations circulate about this developer and are not used anywhere in this document, because they could not be substantiated to the standard above:

1. A community allegation about the developer's earlier work, which rests on a single uncorroborated message.
2. Any claim about the number of source-code questions deleted from the support groups. A deleted message cannot appear in an export, so no count is possible. What is documented instead is the rule that makes the question bannable, and the requests that survived.

**Correction.** Any person named here who disputes a quotation, a date, a hash or a characterisation should [open an issue](../../issues). It will be corrected or removed. The offer has stood since 2026-09-01, on every platform this record has appeared on, and nobody has yet taken it up.

**Contact.** Direct anything arising from this record to [issue 84](https://gitlab.com/rafalense/plus-messenger/-/issues/84) or to this repository's issues. The remedy the licence asks for is source code, and it is obtainable from one person. Approaching anyone named in Chapter 14 undermines the record and helps nobody.

**Scope.** Each action in Chapter 14 is attributed to the account that took it, on the evidence of that account's own public words.

Compiled 2026-09-01 and 2026-09-02.
