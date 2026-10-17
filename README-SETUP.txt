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
  3. Open setup.html in Chrome and fill in the steps:
       area name -> paste firebaseConfig -> staff e-mails (Step 2b) -> choose the GeoJSON
       -> tick GN divisions and type the PHM area of each
       -> press "Save config.js" and "Save area-geo.js".
     Then do what Step 2b says in the Firebase console (enable Email/Password, add the staff
     users, paste the rules and Publish). Without this the database stays open to anybody.
  4. Put config.js and area-geo.js in the SAME folder as index.html.
  5. Open index.html. The GN list, PHM area and map are now for your area.

SECURITY (patient data)
  - The app asks for e-mail + password. Only the e-mail addresses listed in your database
    rules can read/write patient records. Everybody else is refused by Firebase itself.
  - Create the staff accounts in Firebase -> Authentication -> Users -> Add user, and
    turn off "Enable create (sign-up)" if you see that option.
  - When someone leaves: delete their account AND remove the e-mail from the rules.
  - Do NOT copy someone else's config.js (it holds their database key).
  - Never put patient exports / photos in a public GitHub repository.
  - Lock the phone / computer with a PIN: reports are also kept on the device.
  - To change area later, run setup.html again and replace the two files.
  - Gemini API key (for photo reading) is typed inside the app, per user.
