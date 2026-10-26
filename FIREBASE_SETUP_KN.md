# KSEAB SSLC Mathematics App — Online PDF Upload Setup (ಕನ್ನಡ)

ಈ app Netlify ನಲ್ಲಿ static website ಆಗಿರುವುದರಿಂದ PDF ಗಳನ್ನು ಎಲ್ಲ ವಿದ್ಯಾರ್ಥಿಗಳಿಗೆ online ನಲ್ಲಿ ತೋರಿಸಲು cloud storage ಬೇಕು. ಈ ZIP ನಲ್ಲಿ Firebase Authentication + Cloud Firestore + Cloud Storage integration ಸೇರಿಸಲಾಗಿದೆ. **Firebase project configuration ಹಾಕುವವರೆಗೆ upload ಕೆಲಸ ಮಾಡುವುದಿಲ್ಲ.**

## 1. Firebase project ರಚಿಸಿ
1. ಮೊಬೈಲ್ Chrome ನಲ್ಲಿ https://console.firebase.google.com/ ತೆರೆಯಿರಿ ಮತ್ತು Google account ಮೂಲಕ sign in ಮಾಡಿ.
2. **Create a project / Add project** ಒತ್ತಿ. ಹೆಸರು `kseab-sslc-maths` (ಅಥವಾ ನಿಮಗೆ ಇಷ್ಟವಾದ ಹೆಸರು) ನೀಡಿ.
3. Project ಸಿದ್ಧವಾದ ಮೇಲೆ Project Overview → Web icon `</>` ಆಯ್ಕೆ ಮಾಡಿ, app nickname ನೀಡಿ Register app ಒತ್ತಿ.
4. ತೋರಿಸುವ `firebaseConfig` values ಅನ್ನು ಉಳಿಸಿಕೊಳ್ಳಿ. **Service account private key ಬಳಸಬೇಡಿ.**

## 2. Admin login ಸಿದ್ಧಪಡಿಸಿ
1. Firebase → Build → Authentication → Get started → Sign-in method ನಲ್ಲಿ **Email/Password** enable ಮಾಡಿ.
2. Authentication → Users → Add user ಆಯ್ಕೆ ಮಾಡಿ admin email ಮತ್ತು password ಸೃಷ್ಟಿಸಿ. ಈ email ಅನ್ನು ಬೇರೆ ಯಾರಿಗೂ ಹಂಚಬೇಡಿ.
3. `www/firebase-config.js` ಫೈಲ್‌ನಲ್ಲಿ `adminEmails` ಒಳಗೆ ನಿಮ್ಮ admin email ಹಾಕಿ.

## 3. Firestore ಸಕ್ರಿಯಗೊಳಿಸಿ
1. Firebase → Build → Firestore Database → Create database. Production mode ಆಯ್ಕೆ ಮಾಡಿ.
2. Firestore → Rules ತೆರೆಯಿರಿ. ZIP‌ನ `firebase-firestore.rules` ಒಳಗಿನ ನಿಯಮಗಳನ್ನು ಅಂಟಿಸಿ Publish ಒತ್ತಿ.

## 4. Storage ಸಕ್ರಿಯಗೊಳಿಸಿ
1. Firebase → Build → Storage → Get started ಒತ್ತಿ. ಬೇಕಾದರೆ billing/plan ಸೂಚನೆಗಳನ್ನು ಪರಿಶೀಲಿಸಿ; Firebase Storage ಲಭ್ಯತೆ ಮತ್ತು ವೆಚ್ಚವು project/ಪ್ರದೇಶದ ಪ್ರಸ್ತುತ ನಿಯಮಗಳ ಮೇಲೆ ಅವಲಂಬಿತ.
2. Storage → Rules ನಲ್ಲಿ ZIP‌ನ `firebase-storage.rules` ನಿಯಮಗಳನ್ನು ಅಂಟಿಸಿ Publish ಒತ್ತಿ.

## 5. Config values ಹಾಕಿ
`www/firebase-config.js` ತೆರೆಯಿರಿ. Firebase Web App config‌ನ ನಿಜವಾದ values ಹಾಕಿ:
- `apiKey`
- `authDomain`
- `projectId`
- `storageBucket`
- `messagingSenderId`
- `appId`

`YOUR_PROJECT_ID` ಮುಂತಾದ placeholders ಉಳಿಯಬಾರದು. `adminEmails` ನಲ್ಲಿ ನಿಮ್ಮ ನಿಜವಾದ admin email ಇರಲಿ.

## 6. GitHub/Netlify ಗೆ ಪ್ರಕಟಿಸಿ
1. ZIP extract ಮಾಡಿ. `KSEAB_SSLC_Mathematics_App/www/` ಒಳಗಿನ ಫೈಲ್‌ಗಳನ್ನು ನಿಮ್ಮ GitHub repository ಯಲ್ಲಿರುವ ಅದೇ `www/` folder‌ಗೆ upload/replace ಮಾಡಿ. Folder structure ಉಳಿಸಿ.
2. `firebase-config.js` ಸೇರಿರುವುದನ್ನು ಖಚಿತಪಡಿಸಿ. Netlify publish directory `www` ಆಗಿರಲಿ.
3. Netlify deploy ಮುಗಿದ ಮೇಲೆ website refresh ಮಾಡಿ. ಹಳೆಯ cache ಕಾಣಿಸಿದರೆ Chrome ನಲ್ಲಿ site refresh ಮಾಡಿ ಅಥವಾ site data/cache clear ಮಾಡಿ.

## 7. Admin ನಿಂದ PDF upload ಮಾಡುವುದು
1. Website ತೆರೆಯಿರಿ → **Documents / ದಾಖಲೆಗಳು** tab ಒತ್ತಿ.
2. **Admin upload** ಒತ್ತಿ, Firebase Authentication ನಲ್ಲಿ ರಚಿಸಿದ admin email/password ಮೂಲಕ sign in ಮಾಡಿ.
3. Document title, category ಮತ್ತು PDF ಆಯ್ಕೆ ಮಾಡಿ (ಗರಿಷ್ಠ 15 MB). **Upload document** ಒತ್ತಿ.
4. Upload ಯಶಸ್ವಿಯಾದ ಮೇಲೆ PDF ಎಲ್ಲ ವಿದ್ಯಾರ್ಥಿಗಳ Documents ಪಟ್ಟಿಯಲ್ಲಿ ಕಾಣುತ್ತದೆ.

## Security ಗಮನಿಸಿ
ಈ ZIP‌ನ starter rules ನಲ್ಲಿ authenticated users ಬರೆಯಲು ಅನುಮತಿ ಇದೆ. App UI admin email ಅನ್ನು ಪರಿಶೀಲಿಸುತ್ತದೆ, ಆದರೆ client-side ಪರಿಶೀಲನೆ ಮಾತ್ರವೇ ಸಂಪೂರ್ಣ ಭದ್ರತೆ ಅಲ್ಲ. ಸಾರ್ವಜನಿಕವಾಗಿ ಬಳಸುವ ಮೊದಲು Firestore/Storage rules ಅನ್ನು Firebase custom claims ಆಧಾರಿತ admin-only rules ಆಗಿ ಗಟ್ಟಿಗೊಳಿಸುವುದು ಉತ್ತಮ. ವಿದ್ಯಾರ್ಥಿಗಳಿಗೆ Firebase Authentication account ಸೃಷ್ಟಿಸಬೇಡಿ; admin account ಮಾತ್ರ ಸೃಷ್ಟಿಸಿ. Rules ಅನ್ನು ಅರ್ಥಮಾಡಿಕೊಳ್ಳದೆ public write access ತೆರೆಯಬೇಡಿ.

## Troubleshooting
- “Firebase is not configured”: `www/firebase-config.js` ನಲ್ಲಿ values ಬದಲಾಯಿಸಿಲ್ಲ.
- “Permission denied”: Firestore/Storage rules publish ಆಗಿದೆಯೇ ಮತ್ತು admin signed in ಆಗಿದೆಯೇ ಪರಿಶೀಲಿಸಿ.
- PDF upload ನಂತರ ಕಾಣದಿದ್ದರೆ page refresh ಮಾಡಿ, Firestore `documents` collection ಹಾಗೂ Storage `documents/` folder ಪರಿಶೀಲಿಸಿ.
