# How to build اقرأ Steps yourself

This folder is your app project. It is already set up for Android and iPhone/iPad,
with the app icon, splash screen and fonts built in (the app works offline).

You do not need to write code. You only install programs and click buttons.

---

## Part 1 — Android (works on Windows, Mac or Linux)

### 1. Install Android Studio (free)
- Go to developer.android.com/studio and download Android Studio.
- Install it and open it. Let it finish its first-time setup (it downloads extra parts, this can take 15–30 minutes).

### 2. Open the app
- In Android Studio choose **Open**.
- Select the folder **android** that is inside this project folder.
- Wait while it says "Gradle sync" at the bottom. The first time can take several minutes.

### 3. Try it on your phone
- On your Android phone: Settings → About phone → tap **Build number** 7 times. This turns on Developer options.
- Settings → Developer options → turn on **USB debugging**.
- Connect the phone to the computer with a cable and tap **Allow** on the phone.
- In Android Studio, pick your phone at the top, then press the green ▶ **Run** button.
- The app installs on your phone with its own icon.

(No phone? Use Tools → Device Manager → create a virtual phone, then press ▶.)

### 4. Make the file for Google Play
- Menu: **Build → Generate Signed App Bundle / APK** → choose **Android App Bundle** → Next.
- Click **Create new…** to make your key. Choose a place to save it and a password.
  **Keep this key file and password safe forever.** You need the same key for every update.
- Choose **release** → Create.
- When it finishes, click **locate**. Your file is `app-release.aab`.

### 5. Upload it for testing
- Go to play.google.com/console and create a developer account (one-time fee).
- **Create app** → name it, choose **App**, **Free** (you can add subscriptions later).
- Finish the setup checklist: privacy policy, app access, content rating,
  target audience (choose ages under 13 — the app must follow Google's Families policy), data safety.
- Go to **Test and release → Testing → Closed testing** → create a track → **Create new release**
  → upload `app-release.aab` → Save → Review → Start rollout.
- Add your testers' Gmail addresses, copy the **opt-in link**, and send it to them.
- New personal accounts need **at least 12 testers opted in for 14 days in a row**
  before you can apply to publish to everyone.

### Updating the app later
- Put the new `index.html` into the **www** folder (replace the old one).
- Copy the same `index.html` into `android/app/src/main/assets/public/` (replace the old one).
- In `android/app/build.gradle` raise `versionCode` by 1 (for example 1 → 2) and change `versionName` (for example "1.1").
- Build a new signed bundle (step 4, with the **same key**) and upload it as a new release.

---

## Part 2 — iPhone and iPad (needs a Mac — Apple's rule)

### 1. Install the tools on the Mac
- **Xcode** from the Mac App Store (free, large download).
- **Node.js** (LTS version) from nodejs.org.
- **CocoaPods**: open the **Terminal** app and paste:
  `sudo gem install cocoapods`
  (type your Mac password when asked; nothing shows while you type, that's normal)

### 2. Prepare the project
In Terminal, type `cd ` (with a space), drag this project folder into the Terminal window, press Enter. Then paste these, one at a time:

```
npm install
npx cap sync ios
npx cap open ios
```

Xcode opens.

### 3. Try it on your iPhone
- In Xcode click **App** in the left list → **Signing & Capabilities** → **Team** → sign in with your Apple ID.
- Change **Bundle Identifier** to something unique, like `com.yourname.iqrasteps`.
- Connect your iPhone, pick it at the top, press ▶.
  (The first time, on the iPhone: Settings → General → VPN & Device Management → trust your developer profile.)

### 4. Send it to testers with TestFlight
- Join the Apple Developer Program at developer.apple.com (yearly fee).
- In Xcode: choose **Any iOS Device** at the top → menu **Product → Archive** → **Distribute App** → **App Store Connect** → Upload.
- At appstoreconnect.apple.com → your app → **TestFlight** → add testers by email.

---

## Good to know
- **Progress** (stars, children, levels) is saved on each device.
- **Payments** are not connected yet. For the testing stage the app is free; the Parents tab has a
  "Try as a member" switch so testers can see everything. Real subscriptions need Google Play Billing
  and Apple In-App Purchase, which is a later step.
- **App ID**: the project uses `com.iqrasteps.app`. If you want your own, change `appId` in
  `capacitor.config.json` and `applicationId` in `android/app/build.gradle` **before** your first upload.
  It can never change after that.
