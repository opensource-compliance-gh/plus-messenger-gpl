# The Plus Messenger Files: 50M+ downloads and a decade of GPL stonewalling

**In 2014, rafalense admitted hiding code in WhatsApp+ that deleted the `WhatsApp` folders of users running modified builds. In 2016, users warned him that his next messaging client was violating the GPL. In 2017, its source stopped. A decade after the first warnings, Plus Messenger ships a private ad, analytics and billing system to a Google Play audience of 50M+ downloads and sells ad removal for as much as EUR 99.99.**

The current APK contains roughly **11,440 decompiled lines under `org.telegram.plus` that appear in no published source tree**. The private package includes the revenue code and a remotely triggerable test mechanism that can read Telegram login codes and upload them to the developer's Firebase project. That mechanism is gated to two hardcoded phone numbers. Every copy of the examined APK carries it.

The evidence was public: signed artifacts, commit histories, changelogs, pinned rules, store listings and written admissions. [Chapter 12](#chapter-12-verify-all-of-it-yourself) reproduces the technical case in about ten minutes.

The GPL allows forks, modification and commercial distribution. It requires distributors to provide the corresponding source or a written offer. Plus Messenger has provided neither for any release since September 2017. Its official support group tells users not to ask and says the source goes only to “limited parties” such as Telegram. The code flows in from Telegram. It does not flow back out.

Within thirteen hours of submission, moderators and project contributors deleted the reporter's account before publication, closed two complaints, stripped roughly thirty primary-source citations from the surviving copy, and promised cross-platform surveillance. They challenged zero hashes, commits, dates or lines of GPLv2 §3.

## The dossier in 90 seconds

- **2014:** Rafalense admits planting WhatsApp-folder deletion code in WhatsApp+ as an anti-modification measure. HTCMania suspends him and removes his developer title.
- **2015:** He submits Plus Messenger to F-Droid as **GNU GPL v2**. Knowledge of the licence is his own written record.
- **2016:** Users identify the missing-source violation in his support group and explain his obligation to him.
- **2017:** The last corresponding source appears. A group admin concedes that the GPL is not being followed.
- **2018:** Two source requests cite GPLv2 §3. Both remain open and unanswered.
- **2019:** Withholding becomes pinned policy. The rule says source is delayed, limited to selected parties and not a permitted topic of discussion.
- **2025:** The project says withholding prevents others from adding ads. The developer adds ads and paid removal himself.
- **2026:** The current APK exposes an unpublished ad, billing and Firebase backend layer. Store listings tell different monetisation stories. A formal compliance request receives no answer.
- **2 September 2026:** Open-source moderators move faster against the report than anyone moved during a decade of warnings and withheld source.

The fix takes one upload: publish the complete corresponding source, including the ad and billing code, or make and honour a GPLv2 §3(b) written offer.

## Index

- **[Chapter 1: How Plus got here](#chapter-1-how-plus-got-here)**
    - [Before Plus Messenger: the WhatsApp+ deletion trap](#before-plus-messenger-the-whatsapp-deletion-trap)
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
- **[Chapter 13: The report was punished, the evidence went unanswered](#chapter-13-the-report-was-punished-the-evidence-went-unanswered)**
- **[Chapter 14: Wall of shame: moderators who punished the report](#chapter-14-wall-of-shame-moderators-who-punished-the-report)**
    - [14.1 vdbhb59 (`@flossboxin`)](#141-vdbhb59-flossboxin)
    - [14.2 Licaon_Kter](#142-licaon_kter)
    - [14.3 Oswald Boelcke, XDA Senior Moderator](#143-oswald-boelcke-xda-senior-moderator)
    - [14.4 F-Droid forum staff](#144-f-droid-forum-staff)
    - [14.5 The pattern](#145-the-pattern)
- **[Chapter 15: What remains unresolved](#chapter-15-what-remains-unresolved)**
- **[Chapter 16: Requested remediation](#chapter-16-requested-remediation)**
- **[Chapter 17: The record stands](#chapter-17-the-record-stands)**
- **[Before you trust Plus Messenger with your messages](#before-you-trust-plus-messenger-with-your-messages)**
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
| **Author** | Pseudonymous. Not counsel, and none of this is legal advice. Legal analysis and evidentiary limits are identified where they arise. |

---

# Chapter 1: How Plus got here

Plus Messenger is a modified build of **Telegram for Android**, with tabs, multiple accounts, chat categories and theming added. Google Play reports **50M+ downloads** for package `org.telegram.plus`. The current release is 12.10.1.0, dated 2026-08-29. Its upstream is [DrKLO/Telegram](https://github.com/DrKLO/Telegram), © Nikolai Kudashov and contributors, licensed **GPL-2.0-or-later**.

Forking Telegram is allowed. The GPL was written to allow it.

### He calls the app GPL-licensed

His own record rules out the "he didn't know" defence:

1. **His GitLab repository** carries the GPLv2 `LICENSE` file: [gitlab.com/rafalense/plus-messenger](https://gitlab.com/rafalense/plus-messenger) (profile: [gitlab.com/rafalense](https://gitlab.com/rafalense))
2. **His GitHub repository** carries it too: [github.com/rafalense/Plus-Messenger](https://github.com/rafalense/Plus-Messenger) (profile: [github.com/rafalense](https://github.com/rafalense))
3. **He submitted the app to F-Droid himself on 27 March 2015, describing it as "GNU GPL v2"**: https://f-droid.org/forums/topic/plus/

That submission was declined, and the recorded reason concerned bundled Google Play Services rather than the licence. **Remember it.** In Chapter 14, an F-Droid board member deletes this report on the grounds that it has nothing to do with F-Droid.

### Before Plus Messenger: the WhatsApp+ deletion trap

Plus Messenger was not rafalense's first closed messaging mod. He previously built **WhatsApp+** by reverse-engineering WhatsApp's proprietary Android client. In a [May 2014 interview](https://www.softonic.com/articulos/entrevista-whatsapp-plus-uso-ilegal), he acknowledged that the reverse engineering violated WhatsApp's terms. He also sold a EUR 2.59 app called **Plus Donation** that unlocked the ability to hide online status. The “donation” came with a price and a paywalled feature. Even contemporary coverage [called it a purchase in everything but name](https://www.elespanol.com/elandroidelibre/aplicaciones/20140509/whatsapp-version-no-oficial-mejora-original-actualizacion/13748945_0.html).

In November 2014, users of modified WhatsApp+ builds lost photos and videos from their `WhatsApp` folders. The developer then [admitted what he had put in the app](https://www.htcmania.com/archive/index.php/t-930236.html):

> *“En un calentón puse la del borrado de la carpeta WhatsApp sin medir las consecuencias.”*
>
> In a fit of anger, I added the WhatsApp-folder deletion measure without considering the consequences.

He said the deletion code targeted modified version 6.43D, removed it in 6.45D, and apologized to people who lost media. HTCMania's staff later [suspended him for three months, removed his developer title and closed his threads](https://www.htcmania.com/archive/index.php/t-930933.html). Two months later, WhatsApp+ shut down after a [cease-and-desist from WhatsApp](https://techcrunch.com/2015/01/21/whatsapp-cracks-down-on-third-party-apps-temporarily-bans-their-users-from-its-service/).

The sequence deserves to survive the euphemisms. He reverse-engineered somebody else's closed app, sold an unlock for his modification, and planted deletion code when other people modified his modification. Intellectual-property boundaries became sacred one layer down.

That history says nothing about what the current APK does. It makes blind trust absurd. A developer who once hid a retaliation mechanism in a messaging client now asks tens of millions of downloaders to trust nearly a decade of private changes to another messaging client.

### Where he distributes the binary

He lists these himself, in his official FAQ post ([plusmsgrfaq/23](https://t.me/plusmsgrfaq/23), 2020-07-01):

1. **Google Play**, 50M+ installs: https://play.google.com/store/apps/details?id=org.telegram.plus, labelled "Contains ads" and "In-app purchases"
2. **Huawei AppGallery**, 6M installs: https://appgallery.huawei.com/app/C102568417. This listing becomes its own finding in Chapter 9.
3. **APKMirror**: `rafalense/plus-messenger`
4. **Telegram**: https://t.me/plusmsgrupdates
5. **Official site**: https://plusmessenger.org

He distributes the binary in five places. **None offers source.** That is a GPLv2 section 3 failure repeated five ways for nearly a decade, and it is the least serious finding in this document.

---

# Chapter 2: What the licence actually requires

Only the parts that matter to this case. GPLv2, section 3:

> **3.** You may copy and distribute the Program [...] in object code or executable form under the terms of Sections 1 and 2 above provided that you also do one of the following:
>
> **a)** Accompany it with the **complete corresponding** machine-readable source code [...]
>
> **b)** Accompany it with a **written offer**, valid for at least three years, to give **any third party** [...] a complete machine-readable copy of the corresponding source code [...]
>
> [...] For an executable work, **complete source code means all the source code for all modules it contains**, plus any associated interface definition files, **plus the scripts used to control compilation and installation** of the executable.

And section 4, the consequence:

> **4.** [...] Any attempt otherwise to copy, modify, sublicense or distribute the Program is void, and **will automatically terminate your rights** under this License.

A reader checking the licence will also find **3(c)**, which permits passing along the written offer you received. It applies only to noncommercial redistribution of something you did not originate, so the party who created and distributes the work cannot use it.

Four words do all the work here:

| Word | What it means | What it rules out |
|---|---|---|
| **complete** | all modules, plus build scripts | publishing the parts you don't mind sharing |
| **corresponding** | the source of the binary you shipped | publishing an older version instead |
| **any third party** | a 3(b) offer is open to everyone | an offer to a list you approve |
| **accompany** | it travels with the binary | "eventually", or "on request, maybe" |

The licence is not a treasure map. It does not hide a decade-scale delay exception between *complete* and *corresponding*.

Chapter 7 records his own support infrastructure saying, in a rule pinned for seven years, that the source is *delayed*, *partial*, and *available to limited entities such as Telegram*.

---

# Chapter 3: The published source stopped in 2017

His own group rules point users to the GitLab repository as the current one. The complete history, not a selection of it:

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

The GitLab tree did move once after the code stopped: a README edit in 2019, the software equivalent of changing the sign on an abandoned building.

Two people already noticed and filed the obvious issue. Both cite the licence, and both have sat open since **October 2018** without a reply:

- https://gitlab.com/rafalense/plus-messenger/-/issues/20
- https://gitlab.com/rafalense/plus-messenger/-/issues/22

> **Published source:** 4.2.1.1, 2017-09-13  
> **Google Play release:** 12.10.1.0, 2026-08-29

That is eight major versions across a source gap now measured on a decade scale, and section 3 requires source corresponding to the binary being distributed. There is none for anything released since 2017.

A forgotten repository remains possible at this point. [Chapter 4](#chapter-4-the-changelog-says-the-source-is-being-updated) gives that charitable reading about ten more minutes to live. Chapter 11 tests the strongest counter-argument, that the source may match an archived 2017 build.

---

# Chapter 4: The changelog says the source is being updated

### The changelog claim

Every release note carries a line that reads like ongoing compliance:

> *"New in version 10.0.5.0: **Source code updated to v10.0.5**."*
> Source: [plusmsgr/377](https://t.me/plusmsgr/377), 2023-09-07

> *"New in version 12.2.10.0: **Source code updated to v12.2.10**."*
> Source: [plusmsgr/465](https://t.me/plusmsgr/465), 2025-12-10

> *"#stable · **Source code updated to v12.2.10**."*
> Source: [plusmsgrupdates/101](https://t.me/plusmsgrupdates/101), 2025-12-10

Users in his support groups cite these release notes as proof that the app is open source.

### The public repositories

Chapter 3. **Zero code commits since 2017.**

Both statements cannot describe the same event.

### What "source code updated" means

He explains the phrase himself, twice, unprompted:

> *"...**Telegram v10.12 source code has to be published**. Last source code update was a month ago, ...v10.10."*
> Source: [plusmsgr/400](https://t.me/plusmsgr/400), 2024-05-02

> *"Plus Messenger will be updated to v11.6.2 **as soon as Telegram releases source code** based on that version."*
> Source: [plusmsgr/431](https://t.me/plusmsgr/431), 2025-01-21

He is waiting for **Telegram** to publish **Telegram's** source so he can merge it into **his private tree**. "Source code updated to v12.2.10" describes an upstream merge he performed. It is not a release he made.

His changelog hides a possessive pronoun: **my** source code updated. Telegram publishes, he takes, and his users receive a changelog entry announcing that the private tree they cannot inspect has moved again. Open source travels one way here.

The phrase is true in the narrowest sense and misleading in practice. It appears where a user would look for a source release, phrased as a source release would be phrased, in the changelog of an app whose repository has not moved since 2017.

A changelog cannot prove intent. It can show the effect: users read the line as evidence of published source, while the public repository receives nothing.

A stale repository can be a backlog. Monthly announcements that *“source code updated”* while the public tree stays frozen make it a performance.

---

# Chapter 5: The app contains code that has never been published

### Two codebases in one APK

The app on Google Play contains Telegram's GPL code, including features that did not exist before 2026, and the developer's own code, which has never appeared in any repository at any version. His private portion shows ads and takes payments. The licensing boundary and the revenue boundary occupy the same package.

That second category is an advertising engine, an analytics pipeline and a payment system, and none of it can be read by anyone outside the project.

### Evidence

**1. The exact artifact.** Its identity is specific enough to make any disagreement a factual question.

Plus Messenger **12.10.1.0**, `versionCode 22490`, `compileSdk 36 / targetSdk 36`, obtained 2026-09-01 as an XAPK bundle from APKPure, one of the mirrors that redistributes the Play build. The acquisition route matters: this is a mirror copy of the Play artifact, identified by hash, not a capture taken directly from Google Play.

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

The APK carries a **Play App Signing source stamp**, and its app-signing certificate is the one Google Play serves for `org.telegram.plus`. The artifact came through the official distribution pipeline for this package. It is no repack or mirror modification.

It does **not** establish that the developer personally performed the signing. Under [Play App Signing](https://developer.android.com/studio/publish/app-signing), Google holds the app signing key and signs the delivered artifact from an uploaded bundle. The attributable part is what he uploaded and distributes under his account, which is all any argument here requires.

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

The ad controller is present enough to charge the user and absent enough to return HTTP 404.

**6. What that code does to the user.** The in-app **Ads** screen offers Remove Ads, an Enable Ads toggle, Ad placement and Check Purchases. The purchase sheet charges **EUR 5.99** for ad removal, then offers “Remove ads & Donate” tiers at **EUR 11.99, 24.99, 49.99 and 99.99**. All five prices switch off the same unpublished advertising layer. The higher tiers increase the donation.

String resources include `AdsRemoved` and the sales line *"Remove ads and support Plus Messenger project with the approximate price of a coffee/pizza"*, next to copy thanking users for *"all these more than 10 years of free Plus Messenger development"*.

At EUR 99.99, the approximate coffee comes with table service.

**The APK contains `org/telegram/plus/ads/*` while the published source does not contain it, in any version, in either repository.** There is no old copy of this code. There is no copy.

The specific components that convert a messaging client into a revenue stream are the specific components that have never been released.


---

## What the unpublished code actually does

The repository kept `org.telegram.plus` private. The APK was less discreet.

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

### The login-code harvester

`FirebaseHelper` contains a hardcoded array named `test_ids`: **two Spanish mobile numbers, stored Base64-encoded** in the binary. I have not printed them here, because they are personal data and publishing them serves no purpose. Anyone reproducing the decompilation will find them in seconds, and the check that uses them is `isTestId()`.

When the signed-in account's phone number matches one of those two, the app will:

1. Read the **last 20 messages from Telegram peer `777000`**, which is Telegram's official service-notifications account, the account that delivers login codes.
2. Regex-scan them for a 5 to 8 digit code.
3. Write that code, Base64-encoded, into a **Cloud Firestore collection named `tokens`**, in a document named after the account's own phone number, with a server timestamp.

It can also be triggered remotely. `readTopic()` handles incoming push messages, and a push whose payload contains `login` carries `phone` and `code` fields. On such a push, gated by the same two-number check, the app either injects a code into the login flow or kicks off the harvest above.

To feed it, **upstream Telegram's `PushListenerController` was modified in eight places** to pass incoming push text through `FirebaseHelper.isLoginCode()`.

The shipped binary contains a remotely triggerable mechanism that reads Telegram login codes out of the user's own message history and uploads them to the developer's Firebase project. Wiring it up required eight changes to upstream GPL code.

A client-side check gates the mechanism to two hardcoded phone numbers. For any other account, `isTestId()` returns false and nothing is read or uploaded.

The best-supported explanation is a developer automation harness for his own test accounts. The two-number gate supports that reading, and this document uses it.

Every one of those 50,000,000 installs carries the scanner, the Firestore upload path, the push command handler and the modified upstream push controller. The only thing standing between that machinery and any given user is an `if` statement comparing their phone number against a list, in a remotely configurable build whose source the licence has required him to publish since 2017.

The binary doesn't show whether he has ever used the mechanism. Without source history, users cannot see when it appeared or how its gate changed. The GPL source requirement lets the 50 million people running a messaging client find out what it does. A source review would have found this in an afternoon. Instead it sat unseen for as long as it has existed.

### In plain language

Strip away the class names and the decompiler output reduces to a short list.

I downloaded an app with 50M+ Google Play downloads. I ran a decompiler over it. Out came eleven thousand lines of code that has never been published anywhere, and sitting inside it:

1. A live connection to a cloud database the app both reads from and writes to.
2. Anonymous sign-in to the developer's Firebase project, so the app authenticates itself to that backend without the user being asked or told.
3. A remote configuration channel, so what the app does can be changed after you install it, without shipping an update through the store.
4. A push handler that takes instructions, beyond the usual notifications.
5. Its own updater, capable of pulling a new version outside the Play Store.
6. A routine that reads your Telegram service messages, pulls the login code out of them, and writes it to that cloud database in a document named after your phone number.

Number six only fires for two hardcoded phone numbers. I have now said that three times and I will keep saying it every time it comes up, because it's true, and because it's the whole difference between a test harness and something far uglier.

Now look at the rest of the list again. A messaging client with fifty million downloads is carrying a remotely configurable command channel, an authenticated backend connection and an out-of-store updater, in code nobody outside one person has ever read, that the licence has obliged him to publish since 2017.

Plenty of apps ship Firebase. Reviewers would still inspect these capabilities first, especially in an app whose users spent a decade being told it was open source. He published none of them.

### A source diff caught another Telegram fork this year

Five months before this record was compiled, source and binary diverged in another Telegram fork.

On 2026-04-03 it was [reported on r/Android](https://www.reddit.com/r/Android/comments/1sb3h81/nekogram_caught_collecting_user_account/) that **Nekogram** was sending users' phone numbers and usernames to a developer-controlled Telegram bot, via, in the reporter's words:

> "obfuscated injected code **that is not in the source code provided on GitHub**. The packaged APK with the malicious code is distributed via Play Store, GitHub Releases and their Telegram channel."

The report states the developer acknowledged it. A related technical discussion is at [net4people/bbs issue 601](https://github.com/net4people/bbs/issues/601). Nekogram publishes source, so somebody could diff it against the APK and find the injected code.

Plus Messenger cannot be checked that way. It has had no current source to diff since 2017. Documenting its private layer required a slow, lossy manual decompilation that almost nobody performs before installing an app.

This comparison concerns the audit trail. I don't accuse Plus Messenger of the conduct reported in Nekogram. Its login-code path is gated to two hardcoded numbers and does nothing for every other account.

In the same ecosystem and the same year, published source exposed a reported privacy incident. Nekogram got audited. Plus Messenger, with fifty million installs, required somebody to spend an evening running `jadx`.


---

# Chapter 6: There is no written offer either

GPLv2 §3 allows a written offer to supply the source instead of a tarball with every download. Plus Messenger uses neither route.

I searched the decoded app resources for "GNU General Public License", for "source code", and for repository URLs. The complete set of results:

1. A theme-preview joke string.
2. An error message about waiting for Telegram to update its source code.

First-party screenshots of the running app confirm that Settings terminates at a version number, and the Help section contains no licence or source entry. The Play listing carries no source link. `plusmessenger.org` carries no source link.

The app's entire conversation with the GPL consists of a joke string and an error message about waiting for Telegram. Section 3 asked for source or a written offer. It received neither.

---

# Chapter 7: This is a written policy, not an oversight

The rule pinned in 2019 kills the forgotten-repository explanation.

### 2016: the violation is identified correctly, in his own group, with him in it

Ten years ago, in the Spanish support group:

1. [TodoSobrePlusMessenger/7621](https://t.me/TodoSobrePlusMessenger/7621) (2016-09-06): *"supuestamente todas son gpl, pero sacan el código de las que les da la gana y cuando quieren"*
2. [/7623](https://t.me/TodoSobrePlusMessenger/7623) (2016-09-06): going closed-source would "look bad", so they don't, while being held up as a free-software example, *"y no es cierto"*
3. [/10640](https://t.me/TodoSobrePlusMessenger/10640) (2016-09-23): *"si tu quieres conocer el codigo **tienes el derecho a pedirselo** y ellos, al estar bajo cierta licencia, **deben dartelo**"*
4. [/14402](https://t.me/TodoSobrePlusMessenger/14402) (2016-10-05): proposes that Telegram cut off API access for apps that do not honour the licence

The developer is in that group and is addressed directly at [/2718](https://t.me/TodoSobrePlusMessenger/2718) (2016-04-20).

Someone worked out both the violation and the enforcement lever in 2016. Nothing happened. Note item 4 in particular. Chapter 9 is that idea, filed ten years later.

### 2017: a group admin concedes it in writing

> *"La GPL...actualmente **no se cumple**. Pero al ser una licencia basada en copyright solo los Autores del propio código o entidades validados por los autores pueden llevar a acciones legales..."*
> Source: [TodoSobrePlusMessenger/36632](https://t.me/TodoSobrePlusMessenger/36632), 2017-10-21, admin FabianPastor

*The GPL is currently not being complied with, but only the copyright holders can act on it.* Both halves are correct, and the second half is why the first half held to the present. It is also, almost word for word, the conclusion this investigation reached independently in 2026.

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

The arrangement is generous to Telegram: it may inspect the modifications to the GPL code it wrote. The millions receiving the executable are told to stop asking. Section 3 chose the opposite audience.

### The rule is enforced, in English, by an admin

> *"**This is not the place to ask for source code.** Please read the group rules again."*
> Source: [plusmsgrchat/1798149](https://t.me/plusmsgrchat/1798149), 2025-01-22, admin Prowler

The official groups have a second credibility problem: they look padded with bot accounts. Their headline member totals read more like decoration than a reliable count of human support. The project treats those numbers as social proof while its moderation bots quietly remove unwanted messages. Even the audience is a black box.

### People asked anyway, for ten years

- **2021:** A user [asked for current 7.8.x source under the licence](https://t.me/plusmsgrchat/1005599). No source followed.
- **2022:** A volunteer [pointed to the 2017 tree](https://t.me/plusmsgrchat/1175604) and said newer source *“isn't released yet.”* Three months later, another user [named the GPL violation](https://t.me/plusmsgrchat/1231196) outright.
- **2023:** A developer [checked both repositories](https://t.me/TodoSobrePlusMessenger/208400), found both stale and asked for a newer one.
- **2024:** A user asked where the source was, checked the answer and concluded, [*“So it isn't open source. Thanks.”*](https://t.me/TodoSobrePlusMessenger/228653)
- **2025:** One developer [wanted to build on Plus](https://t.me/plusmsgrchat/1840961) and found repositories six and ten years old. Another asked, [*“Is this really closed source?”*](https://t.me/plusmsgrchat/1893817)
- **2026:** A user [asked how to see the source](https://t.me/plusmsgrchat/1992531). The final surviving answer came in May: [Telegram's developers should publish first](https://t.me/plusmsgrchat/2002874).

Different users kept discovering the same locked door. The welcome mat told each one to read the pinned rule.

At least a dozen people asked across ten years and two languages. Several were developers who wanted to build on the app and gave up. A rule pinned for seven years declared the question off-topic, and an admin enforced it in writing. This is policy, not backlog.

Deleted messages cannot be counted. The record proves the rule that makes the question bannable and documents the requests that survived. It makes no claim about how many were removed.

---

# Chapter 8: October 2025, when the stated reason collided with reality

### The stated reason

From the rule pinned since 2019, quoted in full above. The source is withheld to stop third-party developers from using the code:

> *"**en su propio beneficio AGREGANDO PUBLICIDAD**"*
> (for their own benefit, by adding advertising)

### The ad launch

**2 October 2025, 11:42.** His own channel:

> *"Plus Messenger will soon begin showing ads. After more than 10 years of completely free development, this step is necessary to ensure the project's sustainability and continuity. **A small one-time payment will be available to permanently remove [ads]**"*
> Source: [plusmsgr/458](https://t.me/plusmsgr/458) (Spanish: [plusmsgres/436](https://t.me/plusmsgres/436), 11:45)

He added advertising for his own benefit.

The precise act that the withheld source was said to be preventing is the act he performed, using code nobody else can read, in a market nobody else can enter, **because he withheld it**. The stated justification did not fail. It worked as written, for one person.

Users noticed the price before they noticed the irony:

1. [/235555](https://t.me/TodoSobrePlusMessenger/235555) (2025-10-30): *"e pagado para quitar los anuncios pero no se quitan"*
2. [/236619](https://t.me/TodoSobrePlusMessenger/236619) (2025-11-26): paid, then received a Google auto-refund
3. [/237096](https://t.me/TodoSobrePlusMessenger/237096) (2025-12-10): *"he pagado por quitar los anuncios pero...siguen saliendo"*
4. [/237585](https://t.me/TodoSobrePlusMessenger/237585) (2025-12-30): *"ahora...para quitar los anuncios tienes que pagar"*

### And eight months later, the official responder still called it free

> *"**Plus Messenger is not a commercial project**, developer makes it on his own free time and **releases it for free**."* (followed by a donation link)
> Source: [plusmsgrchat/2012183](https://t.me/plusmsgrchat/2012183), 2026-06-11

At the moment that message reached users, the binary from Chapter 5 contained an AdMob integration, a Firebase analytics pipeline, a Play Billing client, a five-tier price ladder topping out at EUR 99.99, and a purchase-restore button.

The word *free* is carrying more weight than the EUR 99.99 tier.

---

# Chapter 9: The same app, a different store, a different story

Telegram's API terms provide a lever that doesn't depend on a copyright holder, and [Chapter 10](#chapter-10-what-was-done-about-it) shows every other door closed.

### Telegram's disclosure rule

Telegram's API Terms of Service, section 3.2, require that you *"clearly mention all the methods of monetization that are used in your app **in all its app store descriptions**."*

### Evidence

| Store | Version | "Contains ads" | "In-app purchases" |
|---|---|---|---|
| Google Play | 12.10.1.0 | **Yes** | **Yes** |
| Huawei AppGallery `C102568417` | 12.7.3.1, updated 2026-06-11 | **No** | **No** |

Both listings captured 2026-09-01. The AppGallery listing carries 6M installs, a "Free" price tag, a plain feature list, and marketing copy stale enough to still claim *"More than 20 million downloads"* and *"One of the best rated messaging apps on Play Store."*

Ads launched around October 2025, and the developer pushed 12.7.3.1 to AppGallery in June 2026 without disclosing any.

Google Play gets the monetisation labels. Huawei gets the “Free” sign and a download count from an earlier decade.

I did **not** download or examine the AppGallery package itself, only the Play-lineage 12.10.1.0 artifact. Huawei could receive a build without AdMob or Play Billing, which would make its listing accurate and dispose of this finding. The developer describes one app across all channels, but confirming the discrepancy requires the AppGallery package.

### Telegram can act without a copyright holder

Unlike the copyright question, **anyone** can raise this with Telegram at `abuse@telegram.org`. Telegram controls API access for third-party clients, so it holds a practical lever that requires neither a lawsuit nor a rights-holder form. It does not require Nikolai Kudashov to feel motivated on a particular Tuesday.

Somebody in that Spanish group worked this out in [2016](https://t.me/TodoSobrePlusMessenger/14402).

---

# Chapter 10: What was done about it

I sent the technical case to the parties able to act on 2026-09-01, before publication.

### Who was notified

1. **The upstream copyright holders.** Telegram, and Nikolai Kudashov personally. They are the only parties who can bring an action or compel a store removal, so I told them first, privately, with the full evidence and a ready-to-file copyright notice they could use or discard.
2. **Licence enforcement organisations.** The bodies that exist for this, given the same evidence and asked whether the analysis holds.
3. **The developer himself**, on his own issue tracker, in public: [issue 84](https://gitlab.com/rafalense/plus-messenger/-/issues/84), opened 2026-09-01 22:16 UTC. It doubles as a formal GPLv2 section 3 source request.
4. **Telegram's abuse channel**, separately, for the section 3.2 disclosure breach in Chapter 9.

I have left out individual recipients, addresses and correspondence. They prove nothing about the developer's conduct, and a contact list would only invite people to pile into somebody's inbox.

### What was asked for

One thing, in every message: **publish the complete corresponding source for the version currently shipped, or ship a written offer.** No damages. No takedown demand. No apology.

### What came back

From the developer: **nothing.** Issue 84 has no reply, which places it alongside issues 20 and 22 from 2018.

Version 12.10.1.0 remains on Google Play, with the same unpublished ad layer, at the same prices.

### The doors that turned out to be locked

I tested every route below live on 2026-09-01. Anyone trying to report a licence violation will meet the same doors.

**Google Play's "Report a policy violation" form.** Selecting the category "Intellectual property" produces the message *"You will not be able to submit this form"* and redirects to the DMCA troubleshooter. The anyone-can-file IP report does not exist in practice.

**Google Play's "Flag as inappropriate".** Six fixed reasons, no free-text field:

1. Content was disturbing
2. Should be for mature audiences only
3. Content felt hostile
4. App felt suspicious
5. I disliked the ads
6. App wasn't what I was looking for

None describes a licence violation. The old "Other objection" box with a description field is gone. I submitted nothing, because filing under a false reason would be worse than filing nothing.

Google accepts *“I disliked the ads.”* It has no box for *“the distributor withheld the source.”* The form has room for taste, not licensing.

**The DMCA route.** Rights-holder only, sworn identity, forwarded to the developer, published to Lumen. Correct for a copyright holder, unusable for anyone else, never filed.

**A public issue on the upstream repository.** DrKLO/Telegram has issues *and* discussions disabled. The GitHub API returns `has_issues=false`, `has_discussions=false`. There is no public way to tell the copyright holder anything on his own tracker.

The formal channels either blocked the report or answered nothing, so I published the record. No conspiracy is needed. Enforcement depends on a copyright holder choosing to act, while the store blocks third-party licence reports.

Nothing malfunctioned. Every part of that system did what it was built to do, and the result is a decade-scale compliance failure with no door to report it through.

---

# Chapter 11: Testing the defences

These are the best defences available, tested against the evidence.

### "Could this simply be a misunderstanding of the licence?"

It would be a reasonable defence for a first-time contributor. It does not fit this record. He shipped a GPLv2 LICENSE file with both repositories, submitted the app to F-Droid as "GNU GPL v2" in 2015 (Chapter 1), and his support group has carried a pinned explanation of *why* the source is withheld since 2019 (Chapter 7). The pinned rationale records deliberate policy.

Six years is a long time for a pinned misunderstanding.

### "Could the published repository correspond to a different build that is still distributed?"

Partly, and it is the fairest point available to him. The published tree is `versionCode 1047` (v4.2.1.1, 2017), and APK archive sites retain historical builds, so the published source may well correspond to an archived 2017 binary that is still downloadable somewhere.

That defence succeeds as far as it goes and no further. Section 3 requires source corresponding to **the binary you distribute**. Google Play serves 12.10.1.0. Source matching a 2017 build discharges the obligation for the 2017 build and nothing after it. Every release from 2017-09-14 onward remains unaccompanied.

The museum piece may have source. The product does not.

### "Could the missing material be legally excluded from 'corresponding source'?"

Section 3 excludes only *"anything that is normally distributed with the major components of the operating system"*. `org.telegram.plus.ads.AdsController` is not a component of Android. It is first-party application code, written by the distributor, running in his process, in his package namespace, driving his revenue. The AdMob and Billing libraries themselves are third-party dependencies and are not the claim here. The claim is his own 954-reference controller class that calls them.

### "Could generated or build-artifact files explain the discrepancy?"

No. Generated files would appear in the binary and be absent from source, which is normal and expected. What is absent here is the entire `org/telegram/plus` package tree: an ads controller, a billing helper, a purchase bottom sheet, a Firebase helper, a drawer UI package and an updater. Those are authored source files, not build output. And section 3 requires *"the scripts used to control compilation and installation"*, so even a pure build-system argument fails on the same sentence.

Build tools generate resource indexes. They do not spontaneously write a billing screen and a 954-reference ad controller.

### "Does Telegram's own licensing situation change the analysis?"

No, and this is his stated defence, so it deserves the fullest answer. Telegram publishes its Android source. He has said, in his own words, that he waits for them ([plusmsgr/431](https://t.me/plusmsgr/431)). But section 3's obligation attaches to *whoever distributes the binary*. Upstream's schedule affects when he can rebase. It has no bearing on whether he publishes **his own** `org.telegram.plus` package and build scripts, which are his work, in his possession, right now.

He waits for Telegram when he wants their code. His own code has spent nearly a decade waiting for him.

### "Is there another source archive somewhere that I missed?"

I checked rather than assumed. His own FAQ post lists his official channels (Chapter 1) and none offers source. His own group rules label the 2017 GitLab repository *"Gitlab [Actual]"*, meaning current. Volunteers answering source questions in 2022 and 2026 pointed to that same repository. If a newer archive exists, the developer, his rules and his volunteers are all unaware of it. **If one is produced, this document will say so.**

### "Was he actually given an opportunity to comply?"

Yes, repeatedly, by many people over ten years (Chapter 7), and formally on 2026-09-01 at [issue 84](https://gitlab.com/rafalense/plus-messenger/-/issues/84) on his own tracker, alongside the unanswered requests from 2018. The remedy requested was publication and nothing else.

### "Could he hold separate permission, or a licence other than the GPL?"

This is the strongest defence available to him, and the document would be dishonest not to state it. A fork's author can hold a separate agreement with upstream rights holders, or a licence on terms other than the GPL, in which case section 3 would not constrain him in the way argued here.

Nothing in the public record indicates any such arrangement: the repositories carry the GPLv2 LICENSE file, the app was represented as GPLv2 in 2015, and the support group's rules discuss the source in licence terms rather than pointing to a private grant. But an arrangement of that kind would not necessarily be public, and only the developer or the rights holders can confirm or exclude it.

**Every conclusion here depends on no such permission existing.** If it exists, saying so resolves the matter faster than publishing the source.

### "Where does the analysis go beyond direct evidence?"

Four places:

1. That "Source code updated to vX" *functions* as a deflection (Chapter 4). The record proves the wording, the zero commits, and his own explanation of what he means by it.
2. That the pattern is policy rather than backlog (Chapter 7). The record proves the pinned rule, its stated rationale, and ten years of deflected requests.
3. That the enforcement vacuum, rather than apathy or coordination, explains the decade-long record (Chapter 10). The record proves that I tested each reporting route and found it closed.
4. That section 4 has terminated the licence (Chapter 16). No court has ruled on it.

Everything else is a link or a hash.

### "Only the copyright holder can complain, so why is a third party doing this?"

Only a copyright holder can sue or force a takedown, which is why Kudashov and Telegram were notified before publication. Section 3 still gives **every recipient of the binary** a right to the corresponding source or to an offer good for any third party. That grants the right to ask and be answered, not standing to sue.

### "It is one person working in his spare time. Leave him alone."

The GPL permits selling. Whether he may earn money from this is not in question and never has been. It attaches one condition, and he has not met it for nearly a decade, while charging up to EUR 99.99. Spare time can explain a schedule. It cannot amend a licence. The payment screen found time to ship.

---

# Chapter 12: Verify all of it yourself

You can reproduce the core findings in roughly ten minutes.

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

**4. The citations.** Open any `t.me/<channel>/<id>` link. Every date given is that message's own timestamp, visible in any Telegram client.

**5. The moderation record.** The two GitLab issues and the GitHub issue linked in Chapter 14. Every quote is on the page.

---

# Chapter 13: The report was punished, the evidence went unanswered

The report reached four open-source venues with an APK hash, a commit history, GPL text and primary-source citations. Their response arrived fast.

Within thirteen hours, moderators and project contributors deleted the reporter's account before the post became public, closed two complaints, stripped roughly thirty citations from the surviving XDA copy, closed that thread, and promised to watch the reporter “in other places.”

The named participants challenged **zero** APK hashes, source commits, dates or lines of the licence. The moderation response found urgency everywhere except the GPL violation.

---

# Chapter 14: Wall of shame: moderators who punished the report

Every name below belongs to a public account exercising public moderation or project authority. The quotations link to the public record. This section judges documented actions, not private motives.

| Account | Power used | Evidence challenged |
|---|---|---|
| vdbhb59 (`@flossboxin`) | Deleted the forum account, sought deletion on another project's tracker, promised cross-platform surveillance | **None** |
| Licaon_Kter | Closed two F-Droid issues, called the conduct report a duplicate, threatened “other measures” | **None** |
| Oswald Boelcke | Removed roughly thirty primary-source citations and closed the XDA thread | **None** |
| Unnamed F-Droid forum staff | Deleted an account without citing a rule, warning or appeal route | **None** |

The table is the whole scandal in miniature. Authority moved within minutes. Scrutiny never reached the evidence.

---

## 14.1 vdbhb59 (`@flossboxin`)

His F-Droid forum profile carries the title **"Contributor, F-Droid Board Member"**, confirmed on 2026-09-02 through [the forum's own JSON](https://forum.f-droid.org/u/vdbhb59.json). He also holds **Developer** access on the [`fdroid/admin`](https://gitlab.com/fdroid/admin/-/issues/700) tracker. He holds no role in the Telegram-FOSS repository, where he demanded deletion two minutes after the F-Droid ban.

At **03:47 UTC**, F-Droid deleted the account that filed this report. The email cited no rule, gave no warning and offered no appeal, saying only that the account *"has been deleted by a staff member."* The post still sat in the new-user queue and had never been publicly visible.

Two minutes later, at **03:49:43**, he turned up under the same report on [a different project's GitHub tracker](https://github.com/Telegram-FOSS-Team/Telegram-FOSS/issues/377#issuecomment-5504070601):

> *"please delete this comment from **the bot above**. The bot has come and posted on several forums. Just created account and posted this. **Banned them. Reporting this as well.**"*

Seven hours later, on F-Droid's own tracker, he explained himself at length:

> *"**I deleted your account, as I saw you as BOT**, which created an account and pasted some links (**including few dubious looking links**) to continue a 6 year old thread... Clickbait."*
>
> *"You shared links to a stale stuff, and **people may click on them out of cusriousity**. Moreover, what you were posting is **old data which people are already aware of**."*
>
> *"**You will remain banned and I will make sure to watch you in other places.**"*

His defence supplied labels instead of a rule: *bot*, *dubious links*, *old data*, *clickbait*. The two “dubious” links went to `gitlab.com` and `github.com`, the repositories under examination. Asked to identify a dangerous link, he named none. Every link in the report resolves to one of eight domains: `t.me`, `gitlab.com`, `github.com`, `play.google.com`, `appgallery.huawei.com`, `f-droid.org`, `plusmessenger.org` or `xdaforums.com`. No shorteners and no redirects.

His warning that users *“may click out of curiosity”* described a threat from a post he prevented users from seeing. Moderation solved the imaginary click before the public got the opportunity to commit it.

The *“old data”* included a SHA-256 computed the previous afternoon. The hash aged twenty-seven hours before F-Droid declared it stale.

The *“6 year old thread”* was a GitHub discussion on another project, not the new forum topic he deleted. His colleague later defended the deletion as an off-topic post. The justification changed. The refusal to examine the evidence did not.

F-Droid's own inclusion policy says the project *"compiles applications from publicly accessible source code to **verify that distributed binaries match their source code**."* That is, word for word, the check documented here. Their Code of Conduct asks members to *"assume good faith"* and reserves bans for *"serious or persistent offenders."* Their forum guidelines prohibit *"Responding to a post's tone instead of its actual content."*

Across everything he wrote about this report, *bot* appears repeatedly. *Source* appears zero times. He evaluated the age of the account, the look of the links and the reporter's future movements. He never evaluated the claim.

A board member of a project built to verify that binaries match public source deleted a report that documented a binary failing that check. He needed two minutes to carry the ban onto another platform and seven hours to write a defence. The source tree received none of that attention.

*“I will make sure to watch you in other places”* is moderation power creep in one sentence. His authority covered an F-Droid forum. He announced a wider jurisdiction for himself and had already followed the report to a repository where he held no role.

The report did not follow him onto GitHub. He followed the report. By then he was no longer protecting an F-Droid moderation queue. He had appointed himself cross-platform hall monitor to a post nobody appears to have created.

---

## 14.2 Licaon_Kter

Licaon_Kter is a long-standing F-Droid contributor with issue-closing rights on [`fdroid/admin`](https://gitlab.com/licaon-kter), the tracker F-Droid's Code of Conduct names for this kind of complaint. The unexplained account deletion arrived there as [issue 700](https://gitlab.com/fdroid/admin/-/issues/700) at 08:13 UTC.

He asked which app in F-Droid this concerned. At **09:03:10** the reporter answered: none, and the reason it is in none is that [rafalense submitted it to F-Droid himself in March 2015, as "GNU GPL v2"](https://f-droid.org/forums/topic/plus/), where it was declined over bundled Play Services.

At **09:04:30**, eighty seconds later, he closed the issue:

> *"ah, ok then"*

Three minutes later, he returned to the closed issue to add:

> *"if your very own FIRST post is an offtopic, sorry... but **I would have deleted your post and account too**"*
>
> *"you even admit knowing that what you did was not proper"*

The 2015 submission did not make Plus Messenger a current F-Droid package. It did establish the direct connection the reporter had just been asked to provide: the same developer had submitted the same GPL fork to F-Droid, and F-Droid had assessed it. Licaon_Kter closed the issue without discussing that history.

A separate Code of Conduct report about the board member's cross-platform conduct opened at 09:14:37 as [issue 701](https://gitlab.com/fdroid/admin/-/issues/701). At 09:27, Licaon_Kter closed that issue too, calling it a *"duplicate of #700"* without comment. Issue 700 challenged an account deletion. Issue 701 challenged a colleague pursuing the reporter onto another project's tracker. Collapsing both into one closed ticket ensured that neither received a separate answer.

He then wrote, on the issue he had closed:

> *"this issue is not locked, no need for other issues, but you can continue to not assume good faith in my posts and **we can take other measures, if you insist**"*
>
> *"the reasoning was simple **'not related to F-Droid, we don't care'**, if you fail to grasp that, there's nothing more to discuss"*

*“We don't care”* might explain why F-Droid declined the licence report. It does not explain why an F-Droid board member cared enough to follow that report onto somebody else's GitHub tracker and demand its deletion. F-Droid was uninterested in the evidence and intensely interested in where it appeared.

Eighty seconds covered the answer, the eleven-year-old submission history and the decision to close. The next three minutes produced a defence of deletion, not a check of the record.

His contribution to the record consists of two closures, a threat of *“other measures”*, and the declaration *“we don't care.”* He did not analyse a single evidence item. Triage achieved a remarkable efficiency: two complaints entered, zero questions survived.

---

## 14.3 Oswald Boelcke, XDA Senior Moderator

The original XDA thread went into the wrong subforum. Senior Moderator **TNSMANI** closed it, then answered a direct question about where the report should go:

> *"The thread looks ok at General Topics."*

That was at 10:39. The replacement went up in General Topics, which is the room a Senior Moderator had just pointed at. At **16:54**, [Oswald Boelcke](https://xdaforums.com/m/oswald-boelcke.7408621/) closed it:

> *"This thread is obviously **a rant about something that occurred or still occurs outside of XDA Forums**. As we don't control anything that happens outside of our website, we don't accept that such rants or fights are posted on our Forums."*
>
> *"In future, don't attempt to carry the trouble, which you experience somewhere on the internet, to our Forums. Your cooperation is appreciated and expected."*
>
> *"Regards  
> Oswald Boelcke  
> Senior Moderator"*

He also wrote:

> *"I've edited your OP and removed the **really extreme number of references to Telegram**."*

The *“really extreme number”* was about thirty `t.me/<group>/<id>` links. They were not invitations or promotions. Each link supported a quoted claim: the pinned source rule, the admin enforcing it, the ads announcement, or users reporting failed ad-removal purchases. They were footnotes with an unfashionable domain name. Every one now reads:

```
{Mod edit: References to Telegram removed!}
```

XDA's rule against Telegram links is real and predates this report. It targets promotion of Telegram groups. Boelcke applied it to primary-source citations, then labelled a post containing GPL text, a commit log, a SHA-256 table and a dex inventory *“obviously a rant.”* Apparently a checksum becomes emotional when it links to Telegram.

The *“trouble somewhere on the internet”* was not a breakup, a feud or a bad restaurant review dragged onto XDA. It was a software-licence compliance report about an Android app, posted on one of the world's largest Android development forums. The GPL is part of the legal machinery that lets developers copy, modify and redistribute free software in the first place. Treating compliance with it as off-site personal drama turns the foundation beneath the forum into *“trouble”* the moment somebody asks whether its terms were honoured.

*“Your cooperation is appreciated and expected”* translated neatly in context: cooperate with the removal of the evidence. The sign-off received three lines. Roughly thirty supporting citations received one deletion notice each.

That thread URL had already gone to licence-enforcement organisations and journalists as the public copy of the evidence. They now reach a page that makes roughly thirty claims without their linked support because a moderator removed the support after the URL went out.

Two Senior Moderators reached opposite conclusions about the same thread inside seven hours, and the cost fell on the person who had asked permission first and then done as he was told.

The rule exists to stop Telegram promotion. On this occasion, it removed evidence that a developer had withheld GPL source for nearly a decade. The result made the *“rant”* label easier to believe: first call the report a rant, then remove the footnotes that let readers discover otherwise.

---

## 14.4 F-Droid forum staff

There is nobody to name because F-Droid does not publish its staff or moderator list. [`forum.f-droid.org/about.json`](https://forum.f-droid.org/about.json) returns empty arrays where those names would appear.

At 03:47, *“a staff member”* deleted the account without citing a rule, warning the user or offering an appeal. The topic never left moderation. The reporter therefore had no stated rule to challenge and no named decision-maker to ask.

The arrangement compresses accountability into a vanishing point: no reason, no name, no appeal. Seven hours and two public issues later, a board member admitted making the deletion. Nobody cited the rule. The ban remains.

---

## 14.5 The pattern

Everything above happened between **03:47 and 16:54 UTC** on 2 September 2026. A forum account disappeared before publication. Two minutes later, a board member appeared on another project's tracker calling the report bot output. A contributor closed the first complaint eighty seconds after receiving the requested context, then closed the conduct complaint as a duplicate. That afternoon, an XDA moderator removed the citations from the last public copy and closed it.

I allege no coordination, and none is needed to explain the record. The tools varied: a spam label, an off-topic rule, duplicate triage and a Telegram-link policy. Each tool landed on the report or reporter. None landed on the nearly decade-old source gap.

Whatever each participant intended, their public actions formed a volunteer shield around the status quo. The developer kept distributing a closed derivative. Every recorded sanction landed on the people and pages documenting it.

Across four venues, none of the named participants quoted a hash, commit, date or licence clause and showed it was wrong. These venues generated more urgency for a new account and forbidden links in thirteen hours than for a decade of warnings and missing source.

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

The developer can erase every item in this list by publishing what the licence already requires. Moderators cannot close that fix as off-topic.

---

# Chapter 16: Requested remediation

The remedy is shorter than the excuse file. Either option closes the matter:

### Option A: publish (GPLv2 §3a)

1. Push the current tree to https://gitlab.com/rafalense/plus-messenger.
2. Include `org/telegram/plus`, the whole package, ads and billing included.
3. Include the build scripts.

### Option B: offer (GPLv2 §3b)

1. Write one paragraph offering the corresponding source to any third party, valid three years.
2. Put it in the Play listing and in the app's About screen.

Option A supplies the source now. Option B commits the developer to supplying it on request for three years.

On a direct reading of section 4, the licence has terminated and distribution continues without one until either remedy occurs. That is legal analysis, not a court ruling.

---

# Chapter 17: The record stands

The source stops in September 2017. The distributed app continues through August 2026. Its current binary combines modern GPL-licensed Telegram code with roughly 11,440 decompiled lines under `org.telegram.plus` that appear in no public source tree. The private portion serves ads, processes analytics and takes payments. No distribution channel carries a written source offer.

Users have requested source since 2016. The support group turned refusal into a pinned rule and claimed withholding would stop other developers from adding ads. In October 2025, the developer added ads. The wall around the code protected one advertiser after all.

GPLv2 §3 doesn't permit the distribution practice documented here. The app takes current upstream code, withholds its corresponding source and monetises the private result. The licence asks for the source. The users ask for the source. The pinned rules tell the users to stop asking.

No named party has identified a false hash, commit, date, quotation or licence clause in this record. Until somebody does, or the source appears, the record stands.

---

# Before you trust Plus Messenger with your messages

Plus Messenger asks for access to conversations, contacts, files, phone numbers and login codes. In return, its developer asks users to trust a binary whose corresponding source has been withheld since 2017.

This record doesn't label the current app malware. The examined binary gates the sensitive login-code mechanism to two hardcoded test numbers. That still leaves a severe trust problem.

The word "open" in a store listing has no value without a chain of checks:

1. **Read** what the program actually does.
2. **Compare** the published source against the binary you were shipped.
3. **See what changed** between one release and the next.
4. **Verify** that the thing running on your phone is the thing the source describes.

GPLv2 §3 keeps that chain intact. It is the inspection mechanism, not paperwork or a demand for credit.

Withholding breaks that chain at the first link. Users no longer run software they can verify. They run software they have decided to trust with less information than the licence promised them.

The licence isn't a privacy policy, and violating it doesn't prove misuse of personal data. It does remove the inspection mechanism that could expose misuse. If the developer won't honour the rule that lets users inspect his code, why assume the unseen code treats their phone number, messages and login credentials with greater care?

Intent does not repair the break. An honest developer can still leave users unable to check, which is why GPLv2 §3 does not contain a good-person exception. Rafalense's WhatsApp+ history makes a demand for blind trust worse, not better.

The Nekogram report began with a diff between published source and the shipped APK. The check worked because the material needed to run it existed.

Plus Messenger has provided nothing current to diff since 2017. The unpublished-code section exists because one person spent an evening running a slow, incomplete decompiler, something few users do before installing an app.

The installation decision belongs to the user. The description does not: Plus Messenger is a closed, trust-me binary built from GPL code whose corresponding source remains withheld. Publishing the source would end that description today.

---

## Notice

**Mirrors.** This record is published at:

- https://github.com/opensource-compliance-gh/plus-messenger-gpl
- https://codeberg.org/opensourcecompliance/plus-messenger-gpl
- https://opensourcecompliance.codeberg.page/plus-messenger-gpl/

**Nature of this document.** A compliance record compiled by a recipient of the binary, exercising the right that GPLv2 section 3 gives every recipient. The author is not a lawyer and this is not legal advice. The section 4 analysis appears in Chapter 16. No court has ruled on it.

**Rights holders.** Only the upstream copyright holders can bring an action or compel a store removal. I notified them on 2026-09-01, before publishing any part of this record, and nothing here is filed on their behalf or with their authority.

**Disputed facts.** Anyone named here who disputes a quotation, a date, a hash or a characterisation should [open an issue](../../issues), and I will correct or remove it.

**Contact.** Direct anything arising from this record to [issue 84](https://gitlab.com/rafalense/plus-messenger/-/issues/84) or to this repository's issues. The remedy the licence asks for is source code, and it is obtainable from one person. Approaching anyone named in Chapter 14 undermines the record and helps nobody.

**Scope.** Each action in Chapter 14 is attributed to the account that took it, on the evidence of that account's own public words.

Compiled 2026-09-01 and 2026-09-02.
