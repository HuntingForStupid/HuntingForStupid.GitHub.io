Note:
@PawPawHacks/Tom Fieber:
If there is an admin account active for a lab, the credentials are admin:admin123

HINT: Broken Access Control.

1. I launched Burp.

2. I checked to see if there was an admin login using the set/known creds, and there was.  I logged out of that for now.

3. The video walkthrough from PawPawHacks/Tom Fieber said that you will want to create two user accounts for this challenge, so that's the first thing I did.  To create two accounts, I made one user account (Tester1), and then launched a "New Incognito window" and created a second user account (Tester2).

4. Over in my Burp proxy window, I colored my Tester1 traffic in purple, and Tester2 in blue.

5. Next, I noted that Tester1 had an ID of "5", and Tester2 had an ID of "6".

6. Once logged in, the platform behaved a lot like PasteBin so, I poked around a bit, trying to see everything I could do with the app and generating some traffic to view via the proxy.  I created some "Snippets", made some "Public", and then went into the "Profile" for Tester2 and under "ACCOUNT SETTINGS", I added a Bio plus I also changed the password.

7. Next, over in my Burp proxy window, I found the "PUT /api/profile/password" traffic. I highlighted that line and right-clicked and selected "Send to Repeater".

8. Now, over in the "Replay" tab, I hit the "Send" button so that we have a baseline of what the traffic "Response" looks like.

9. Still in the "Replay" tab, I changed the ID from "6", to "5", for the other user (Tester2) and hit the red "Send" button.

10. Next, I logged out of my Tester1 account, and logged back in using the other Tester2 account with its new updated password, for the flag!

bug{***}

---
