#Design Prototypes with a Real Database
This template enables you to quickly spin up a new application that is powered by a real database. This allows you to not only separate data from your design, but also gives you persistent data with which you can create multi-screen prototypes and workflows.

###Notes
- This prototype does not have database authentication, which means that anyone with access to your firebase_URL can read and write to your entire database. Probably fine for prototyping purposes, but be wary of using sensitive data.
- This prototype has basic authentication via Staticfile.auth, which works only if the app is deployed using Pivotal Cloud Foundry using the Static File Buildpack. The default user/password is admin/admin. To generate your own encrypted password, use http://www.htaccesstools.com/htpasswd-generator

##Getting Started
+ Open terminal
+ Clone or download repo to your local machine
+ Navigate into your new repository via terminal
+ Start a simple server: `python -m SimpleHTTPServer 8000`
+ Spin up new Firebase Project : https://firebase.google.com/
+ Add your new project's configuration variables into index.html into the 'Initialize Firebase' section (shown below). To find your project's configuration variables, go to the project overview page in the Firebase console and click 'Add Firebase to your web app'. A popup containing the necessary values will appear.
    ```
    // Initialize Firebase
    var config = {
        apiKey: "YOUR KEY HERE",
        authDomain: "YOUR DOMAIN HERE",
        databaseURL: "YOUR DB URL HERE",
        storageBucket: "YOUR STORAGE URL HERE",
    };
    firebase.initializeApp(config);
    ```
+ Next, add the same configuration variables to tasklist.html in order to make sure this page is protected by authentication. 
+ Now edit tasklist.html by inserting your new Firebase Database URL into the placeholder as shown below. You can find this URL at the top of the Database configuration page in the Firebase Console.
    ```
     var myFirebaseRef = new Firebase("YOUR FIREBASE DB URL");
    ```
+ In the Firebase Console, navigate to the Rules tab within the Database page and change the following rules to disallow read/write access unless the user is authenticated: 
    ```
    {
      "rules": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    }
    ```

+ Test connection to DB by adding a new task and seeing the task inside your Firebase console