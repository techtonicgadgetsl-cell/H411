HEALTH 411 - HOW TO SET UP FOR YOUR OWN AREA
=============================================

Files in this folder
  index.html        main report entry page (open this every day)
  disease-map.html  disease location map (button inside index.html)
  setup.html        one-time setup wizard
  form-page1.jpg / form-page2.jpg   the H411 form pictures used for printing
  config.js + area-geo.js           YOUR area settings (made by setup.html in step 3)

ONE-TIME SETUP (about 15 minutes)
  1. Make your own Firebase database
       - console.firebase.google.com -> Add project
       - Build -> Realtime Database -> Create database
       - Project settings -> Your apps -> Web (</>) -> copy the firebaseConfig block
     (Your own project = your patient data stays separate from other PHIs.)
  2. Get your area GeoJSON (GN divisions as polygons) from your office / GIS unit.
  3. Open setup.html in Chrome and fill in the 5 steps:
       area name -> paste firebaseConfig -> choose the GeoJSON -> tick GN divisions
       and type the PHM area of each -> press "Save config.js" and "Save area-geo.js".
  4. Put config.js and area-geo.js in the SAME folder as index.html.
  5. Open index.html. The GN list, PHM area and map are now for your area.

IMPORTANT
  - Do NOT copy someone else's config.js (it holds their database key).
  - Patient data is sensitive. Do not share your page link publicly, and set
    your Firebase database rules so that not everybody can read it.
  - To change area later, run setup.html again and replace the two files.
  - Gemini API key (for photo reading) is typed inside the app, per user.


///////////////////////////////////////////////////////////////////////////////////////////////
Firebase Rules set and Database make

Aluth PHI kenekta database eka hadanna wenama Firebase project ekak ona. Oyage project eken eka wenas karala dennath ona. App eka login nathuwa health_reports kiyana path eka read/write karanawa, nisa rules walata eka denna ona.

A. Aluth PHI ge setup eka (one-time, minutes 15k)
console.firebase.google.com ekata PHI ge own Google account eken login wenna.
Add project gihin nama ekak denna (ex: h411-godigamuwa). Google Analytics ona na.
Left menu eke Build → Realtime Database → Create Database.
Location: Singapore (asia-southeast1).
Mode: Locked mode.
⚙️ Project settings → General → Your apps → Web (</>) click karala app ekak register karanna. Ethakota firebaseConfig = {...} block eka enawa. databaseURL eka nethnam Realtime Database page eken copy karanna.
setup.html open karala:
Step 1: area name.
Step 2: firebaseConfig eka paste karanna.
Step 3: ge area eke GeoJSON eka denna (office / GIS unit eken ganna).
Step 4: GN divisions tick karala PHM area type karanna.
Step 5: config.js saha area-geo.js save karanna.
Ema files 2 index.html thiyena folder ekata dala host karanna. Hosting HTTPS ona, ethakota GPS weda karanawa. Free ekak: Firebase Hosting ho GitHub Pages.

Oyage config.js eka aluth PHI ta denna epa. Eke oyage database key eka thiyenawa.

B. Database Rules

Realtime Database → Rules tab ekata gihin Publish karanna.

Dan thiyena widiya (app eka login nathuwa weda karanna ona): palaweni ekata rules mehema damma:

json
{
  "rules": {
    "health_reports": {
      ".read": true,
      ".write": true,
      ".indexOn": []
    }
  }
}

Eka thama open rules. Link eka danna ayata patient data balanna, wenas karanna, delete karanna puluwan. Link eka WhatsApp group ho public eke danna epa. Staff walata witharak denna.

Hodata karanna puluwan widiya: App ekata Firebase Authentication ekak damala rules wenas karanna ona:

json
{
  "rules": {
    "health_reports": {
      ".read": "auth != null",
      ".write": "auth != null"
    }
  }
}

Ekata app eke login screen ekak ona (Authentication → Email/Password on karala PHI ge email/password ekak hadanna). Dan app eke eka nathi nisa ekata code eka wenas karanna ona.

Oyata ona nam mama login (Email/Password) feature eka add karala rules wala auth != null use karanna puluwan widiya hadala dennam. Kiyanna.
