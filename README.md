# KSEAB SSLC Mathematics — Android + mobile web starter

A bilingual (Kannada/English) study app starter with:
- 15 chapter overview pages with key ideas, formula reminders and worked examples
- Kannada/English toggle
- MCQ quizzes with explanations and score tracking
- Sample practice sets
- Formula book
- PWA install support and service-worker caching for offline use after the first successful load
- Capacitor setup for packaging the same web app as an Android application

## Important content note
This is an independent learning aid, not an official KSEAB app. The included chapters are a starter outline of commonly taught Class 10 mathematics topics; the exact chapter list, names and order can vary by textbook/academic year. The question sets in this project are **sample practice questions**, not authentic previous-year KSEAB papers. Before publication, cross-check the current KSEAB/DSERT syllabus and add licensed/official PDFs and verified answer keys. Do not label sample sets as official papers.

## 1. Run the mobile website locally
Install Node.js LTS, then from this project folder run:

```bash
npm install
npm run start
```

Vite prints a local URL. Open it in your browser. For testing on a phone connected to the same Wi-Fi, use the network URL printed by Vite. Keep the computer's firewall configured to allow local testing.

For a production build:
```bash
npm run build
```
The static site is created in `dist/`. Deploy the **contents** of `dist/` to a static web host over HTTPS. HTTPS (or localhost) is required for service workers and reliable offline caching.

## 2. Install as a mobile web app (PWA)
Open the deployed HTTPS site in a supported browser on Android, then use the browser's “Install app” or “Add to Home screen” menu. Some browsers show the app's install button when the PWA install prompt is available. Open the app online once so its core files can be cached. The Google Fonts stylesheet is optional; text uses system fallback fonts if offline.

## 3. Build the Android APK
Prerequisites:
- Node.js LTS and npm
- Android Studio with a compatible Android SDK
- A JDK version supported by your installed Android Gradle Plugin (Android Studio's bundled JDK is usually easiest)

Run:
```bash
npm install
npm run build
npx cap add android
npx cap sync android
npx cap open android
```
In Android Studio, let Gradle sync finish. To test, select an emulator or USB-connected Android device and press Run. To create an APK, use **Build > Build Bundle(s) / APK(s) > Build APK(s)**. For Play Store release, use **Build > Generate Signed Bundle / APK** and keep the signing key secure.

If the `android/` folder is already created, do not run `npx cap add android` again; use `npx cap sync android`.

## 4. Add authentic previous-year papers
1. Obtain papers from an official KSEAB source or a source whose use is permitted.
2. Verify academic year, exam/subject, language medium and answer key.
3. Put the PDFs under `www/papers/` before building (and add them to the service worker asset list if they must be available offline).
4. Replace sample-paper buttons with links to those verified PDFs. Avoid scraping or redistributing material without permission.

## 5. Content structure
- `www/index.html` — app layout
- `www/styles.css` — responsive styling
- `www/app.js` — language toggle, navigation, quizzes and local progress
- `www/data/chapters.json` — chapter notes, formulas and worked examples
- `www/data/questions.json` — editable MCQ question bank
- `www/data/formulas.json` — formula book
- `www/sw.js` — offline cache rules
- `capacitor.config.json` — Android wrapper configuration

## 6. Offline and data notes
Chapter data and quiz scores are stored locally in the app/browser. Clearing browser/app storage can clear progress. Updating the service worker cache version (`CACHE` in `www/sw.js`) helps devices download updated app files after a release. First load requires an internet connection for the hosted site; subsequent loads work offline once cached.

## 7. Suggested pre-release checklist
- Verify the current official syllabus and all chapter names with KSEAB/DSERT.
- Have a Kannada-language educator review every Kannada translation and mathematical notation.
- Add the complete textbook exercises and worked solutions only from sources you have permission to use.
- Add actual previous-year papers and check answer keys.
- Test on small Android screens, airplane mode, and a fresh install.
- Add accessibility labels, privacy information, app icon/branding approval and a versioned content-update process.
