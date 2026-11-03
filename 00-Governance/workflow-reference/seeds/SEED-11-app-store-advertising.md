---
id: SEED-11
version: "1.0"
status: approved
owner: OP
based_on: []
requirements: []
source_file: "app_store_advertising.md"
---

# App Store Advertising

**Yes, absolutely.** This strategy is known in the industry as **in-house cross-promotion** (or a **first-party walled garden**).

Major mobile publishers—such as King, Playtika, The New York Times, and Zynga—frequently use this model to circulate audiences across their ecosystem without paying third-party ad networks or exposing their brand to ad fraud.

---

### How In-House Cross-Promotion Works

Instead of integrating external ad mediation SDKs (like Google AdMob, Unity, or AppLovin), the media company controls the entire pipeline end-to-end:

* **First-Party Ad Serving:** You build your own lightweight banner, interstitial, or native promo module inside each app.
* **Direct Deep Linking:** When a user taps a promo in App 1, the app checks if App 2 is already installed. If it is, a deep link opens App 2 directly; if not, it opens the app's official Apple App Store or Google Play Store listing.
* **Zero External Intermediaries:** Because the ads are hardcoded or served via your own backend API, no external demand-side platforms (DSPs), supply-side platforms (SSPs), or auction exchanges ever touch the creative or user traffic.

---

### How This Eliminates Fraud and Third-Party Risks

By restricting advertising exclusively to your own apps, you solve virtually every major ad fraud vulnerability:

1. **Immunity from Clickjacking & Fake Close Buttons:** Because your internal development team codes the dismiss buttons, close hitboxes, and navigation logic, there are no rogue SDKs or invisible overlay layers hijacking user taps.
2. **Zero Bot Clicks & Impression Fraud:** You are not paying for cost-per-click (CPC) or cost-per-impression (CPM) inventory on open exchanges. A bot ring cannot siphon your marketing budget because there is no ad auction to manipulate.
3. **No Domain Spoofing or Laundering:** Your brand assets cannot be scraped or used by rogue arbitrageurs on "Made-for-Advertising" (MFA) websites.
4. **App Tracking Transparency (ATT) & Privacy Exemption:** Under Apple’s privacy rules, tracking a user across apps owned by the **same developer account/legal entity** is generally classified as first-party data rather than third-party tracking. You do not need to share device identifiers with external ad networks.

---

### App Store Policies & Compliance Rules

Both Apple and Google permit developers to cross-promote their own catalog, provided you adhere to basic store policies:

* **User Experience & Non-Disruptive Ads:** Promos cannot block core app functionality or lock the screen without an obvious, functional exit. Google Play’s *Disruptive Ads Policy* and Apple's *Human Interface Guidelines* apply equally to internal promotions.
* **No Forced / Deceptive Installs:** You cannot trick users into downloading your other 6 apps (e.g., claiming an update is required or disguising a download prompt as a system error).
* **Store Review Guidelines:** In Apple’s App Store, your apps must each have standalone utility and value. Apple prohibits uploading multiple near-identical "template" apps under Guideline 4.3 (Spam) solely to act as feeder funnels for one primary app.

---

### The Strategic Trade-Off: Safety vs. Growth

While this strategy provides total brand safety and zero media fraud, it introduces a business bottleneck:

| Advantage | Limitation |
| --- | --- |
| **$0 Media Cost:** You pay no auction fees or platform commissions for ad impressions. | **The "Cold Start" Problem:** If App 1 has zero users, it cannot promote Apps 2 through 7. You need an initial audience base for cross-promotion to work. |
| **Total Brand Safety:** No third-party malware, clickbait, or unclosable ads ruin your user experience. | **Audience Cannibalization:** Promoting App 2 inside App 1 might pull an active, paying user out of App 1 rather than generating net-new demand. |
| **First-Party Analytics:** Attribution is tracked cleanly through your own database without third-party tracking cookies or MMP discrepancies. | **Capped Scale:** You can only reach people who already know your brand. To grow beyond that pool, you eventually need organic SEO/ASO, PR, or selective external acquisition. |

### The Standard Industry Playbook

Most studios solve this by using **organic search, ASO, and PR to acquire the initial cohort of users into one "flagship" app**, and then relying on in-house cross-promotion to cross-pollinate those users across the remaining 6 apps for free.

____________________________________________________________________________________________________________________________

**Yes, but you must distinguish between getting users to *try* your app at mass versus getting them to *publicly review* it at mass.**

You can legally pay, reward, or incentivize thousands of people to install, test, and provide private feedback. However, **paying or incentivizing users to leave public ratings or reviews on app stores is illegal under FTC regulations and strictly banned by Apple and Google.**

To scale both adoption and reviews without risking developer account termination or regulatory fines, developers use several compliant frameworks:

---

### Part 1: Getting Users to Try Your App at Mass (Legal & Compliant)

There are zero legal restrictions against incentivizing or paying people to test software, provided feedback stays within testing environments.

#### 1. Professional User Testing Panels & Paid Research

Platforms maintain pools of hundreds of thousands of pre-screened participants who are paid to install your build, complete tasks, and give detailed feedback:

* **UserTesting / UserZoom:** Enterprise platforms for recorded screen walkthroughs, usability surveys, and spoken "think-aloud" feedback across desktop and mobile.
* **PlaytestCloud:** Built specifically for mobile games and interactive consumer apps, delivering gameplay videos, audio commentary, and bug telemetry.
* **User Interviews & Respondent.io:** Source targeted demographics (e.g., enterprise accountants, fitness enthusiasts, students) to test workflows for gift card incentives.
* *Why it's compliant:* Participants test via unlisted test builds (TestFlight / APKs). They submit private bug reports and qualitative feedback—never public app store reviews.

#### 2. Mass Beta Programs (Apple TestFlight & Google Play Closed Testing)

* **Apple TestFlight:** Allows public invitation links supporting up to **10,000 external testers** per build. Testers can take screenshots and submit bug logs directly to App Store Connect.
* **Google Play Closed/Open Testing:** Google requires new personal developer accounts to run a closed test with at least 20 testers for 14 days before production access. You can expand this to thousands via Google Play Open Beta tracks.

#### 3. Rewarded Discovery Platforms (Offerwalls)

* Platforms like **Swagbucks**, **Mistplay**, **Freecash**, or **Tapjoy** pay users small rewards (points, gift cards) to install an app and reach a certain milestone (e.g., "Install and reach Level 10" or "Sign up and create a watchlist").
* *The Rule:* You can pay them to **try/play** the app. You **cannot** require them to leave an App Store rating to collect their reward.

---

### Part 2: Converting Mass Testers into Public Reviews (The Safe Playbook)

Because you cannot buy public reviews, compensate users for stars, or use "review gating" (filtering bad reviews to an internal form while sending 5-star users to the App Store), you must scale reviews through **behavioral optimization**:

#### 1. In-App Rating APIs Triggered at Peak Satisfaction

Never ask for a review on app launch or during setup. Trigger the official native review prompt (`SKStoreReviewController` on iOS and `In-App Review API` on Android) immediately after a **"value event"**:

* *E-commerce:* Right after a package arrives or is marked delivered.
* *Productivity:* Right after exporting a completed report or crossing off all daily tasks.
* *Fitness:* Right after hitting a 7-day workout streak or setting a personal best.
* *Compliance:* The native store dialog lets users submit a 1-to-5 star rating in two taps **without leaving the app**. It is completely randomized by the OS, meaning you never filter or inspect the sentiment.

#### 2. Community Beta-to-Launch Launch Teams

* Gather a core group of several hundred testers on **Discord**, **Slack**, or a **Reddit community** during your beta phase.
* When the app officially goes live to the public, post an announcement asking the community: *"We’re live on the App Store today! If you’ve enjoyed testing the app over the last month, we’d love your honest rating and review."*
* *Compliance:* As long as no financial reward, contest entry, or in-app perk is conditioned on posting the review, asking your active community for honest reviews is standard and completely legal.

#### 3. Closing the Feedback Loop (Developer Replies)

* Publicly replying to every negative or critical review on the App Store and Google Play often converts dissatisfied users into positive raters.
* When you push an update fixing a reported bug, update your reply to that user stating the issue has been resolved. Data across both app stores shows that users who receive a thoughtful developer reply are significantly more likely to update a 1-star rating to 4 or 5 stars.

---

### What Crosses the Line into Illegal Practice?

| Practice | Status | Consequence |
| --- | --- | --- |
| **Paying a testing panel to test your app and write bug reports** | ✅ **100% Legal & Compliant** | Standard software development practice. |
| **Prompting all active users neutrally via official store APIs** | ✅ **100% Legal & Compliant** | Built and supported by Apple and Google. |
| **Giving users 500 in-app gems / $5 credit to leave a review** | ❌ **Strictly Prohibited** | FTC enforcement ($50k+ per violation); app store delisting. |
| **Review Gating:** *"Rate us! (1-3 stars goes to support, 4-5 goes to App Store)"* | ❌ **Prohibited by Store Guidelines** | App rejection during App Store review; flagged for review manipulation. |
| **Hiring a third-party agency offering "1,000 Guaranteed 5-Star Reviews"** | ❌ **Illegal & Fraudulent** | Violates FTC Rule 16 CFR Part 465; permanent developer account ban. |

____________________________________________________________________________________________________________________________

**Yes, but you must distinguish between getting users to *try* your app at mass versus getting them to *publicly review* it at mass.**

You can legally pay, reward, or incentivize thousands of people to install, test, and provide private feedback. However, **paying or incentivizing users to leave public ratings or reviews on app stores is illegal under FTC regulations and strictly banned by Apple and Google.**

To scale both adoption and reviews without risking developer account termination or regulatory fines, developers use several compliant frameworks:

---

### Part 1: Getting Users to Try Your App at Mass (Legal & Compliant)

There are zero legal restrictions against incentivizing or paying people to test software, provided feedback stays within testing environments.

#### 1. Professional User Testing Panels & Paid Research

Platforms maintain pools of hundreds of thousands of pre-screened participants who are paid to install your build, complete tasks, and give detailed feedback:

* **UserTesting / UserZoom:** Enterprise platforms for recorded screen walkthroughs, usability surveys, and spoken "think-aloud" feedback across desktop and mobile.
* **PlaytestCloud:** Built specifically for mobile games and interactive consumer apps, delivering gameplay videos, audio commentary, and bug telemetry.
* **User Interviews & Respondent.io:** Source targeted demographics (e.g., enterprise accountants, fitness enthusiasts, students) to test workflows for gift card incentives.
* *Why it's compliant:* Participants test via unlisted test builds (TestFlight / APKs). They submit private bug reports and qualitative feedback—never public app store reviews.

#### 2. Mass Beta Programs (Apple TestFlight & Google Play Closed Testing)

* **Apple TestFlight:** Allows public invitation links supporting up to **10,000 external testers** per build. Testers can take screenshots and submit bug logs directly to App Store Connect.
* **Google Play Closed/Open Testing:** Google requires new personal developer accounts to run a closed test with at least 20 testers for 14 days before production access. You can expand this to thousands via Google Play Open Beta tracks.

#### 3. Rewarded Discovery Platforms (Offerwalls)

* Platforms like **Swagbucks**, **Mistplay**, **Freecash**, or **Tapjoy** pay users small rewards (points, gift cards) to install an app and reach a certain milestone (e.g., "Install and reach Level 10" or "Sign up and create a watchlist").
* *The Rule:* You can pay them to **try/play** the app. You **cannot** require them to leave an App Store rating to collect their reward.

---

### Part 2: Converting Mass Testers into Public Reviews (The Safe Playbook)

Because you cannot buy public reviews, compensate users for stars, or use "review gating" (filtering bad reviews to an internal form while sending 5-star users to the App Store), you must scale reviews through **behavioral optimization**:

#### 1. In-App Rating APIs Triggered at Peak Satisfaction

Never ask for a review on app launch or during setup. Trigger the official native review prompt (`SKStoreReviewController` on iOS and `In-App Review API` on Android) immediately after a **"value event"**:

* *E-commerce:* Right after a package arrives or is marked delivered.
* *Productivity:* Right after exporting a completed report or crossing off all daily tasks.
* *Fitness:* Right after hitting a 7-day workout streak or setting a personal best.
* *Compliance:* The native store dialog lets users submit a 1-to-5 star rating in two taps **without leaving the app**. It is completely randomized by the OS, meaning you never filter or inspect the sentiment.

#### 2. Community Beta-to-Launch Launch Teams

* Gather a core group of several hundred testers on **Discord**, **Slack**, or a **Reddit community** during your beta phase.
* When the app officially goes live to the public, post an announcement asking the community: *"We’re live on the App Store today! If you’ve enjoyed testing the app over the last month, we’d love your honest rating and review."*
* *Compliance:* As long as no financial reward, contest entry, or in-app perk is conditioned on posting the review, asking your active community for honest reviews is standard and completely legal.

#### 3. Closing the Feedback Loop (Developer Replies)

* Publicly replying to every negative or critical review on the App Store and Google Play often converts dissatisfied users into positive raters.
* When you push an update fixing a reported bug, update your reply to that user stating the issue has been resolved. Data across both app stores shows that users who receive a thoughtful developer reply are significantly more likely to update a 1-star rating to 4 or 5 stars.

---

### What Crosses the Line into Illegal Practice?

| Practice | Status | Consequence |
| --- | --- | --- |
| **Paying a testing panel to test your app and write bug reports** | ✅ **100% Legal & Compliant** | Standard software development practice. |
| **Prompting all active users neutrally via official store APIs** | ✅ **100% Legal & Compliant** | Built and supported by Apple and Google. |
| **Giving users 500 in-app gems / $5 credit to leave a review** | ❌ **Strictly Prohibited** | FTC enforcement ($50k+ per violation); app store delisting. |
| **Review Gating:** *"Rate us! (1-3 stars goes to support, 4-5 goes to App Store)"* | ❌ **Prohibited by Store Guidelines** | App rejection during App Store review; flagged for review manipulation. |
| **Hiring a third-party agency offering "1,000 Guaranteed 5-Star Reviews"** | ❌ **Illegal & Fraudulent** | Violates FTC Rule 16 CFR Part 465; permanent developer account ban. |
