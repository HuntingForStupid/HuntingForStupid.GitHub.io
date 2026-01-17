# icanhaspii-CTF CheatSheet ## These are my CTF Hacks! I hope you enjoy!
[Details

Details

[Pcap Analysis]](https://lab-1768516934025-kmg7su.labs-app.bugforge.io

PawPawHacks/Tom Fieber Walkthrough:
???

Shadowforge WriteUp:
https://shadowforge.gitbook.io/shadowforge-writeups/bugforge.io/readme.txt/daily-labs/legacy-endpoints/sokudo

BlackM4C WriteUp:
???

7s26simon WriteUp:
???

Moza writeUp:

Ruur/Leonel Obina WriteUp:
???

0ber1n WriteUp:
???

ShadeHawk WriteUp:
???

Pascuale, Federico WriteUp:
???

John Matrix WriteUp:
https://johnmatrix.org/BugForge/Sokudo

b4sh0xf/Gustavo Linhares Writeup:
https://b4sh0xf.github.io/writeups/bs/sokudo

HINT: Can you find API endpoints on a different path? (Legacy Endpoints)

Note:
pawpawhacks 🎄
If there is an admin account active for a lab, the credentials are admin:admin123

1. I launched Caido.

2. I checked to see if there was an admin login using the set/known creds, but there was not.

3. I created a user account, and once logged in, the app appeared to be an online platform to test your typing speed. I tried to do everything I could with the app, in order to generate some traffic to view via the proxy.  I took a couple typing tests, viewed the Dashboard, checked my stats, etc.

4. Over in my Caido proxy window, I noticed traffic for "POST /v2/register" and "GET /v2/stats" which led me to wonder if there was a v1 (version 1) which might have been left hanging around after an update, so I highlighted the "GET /v2/stats", then right-clicked and selected, "Send to Replay -> Default Collection".

5. Next, moving over to the "Replay" tab, I hit the "Send" button so that we would have a baseline of what the traffic "Response" looked like.

6. I tried to see if there was anything to be gained by changing the v2 to v1, but I didn't discover anything notable:

GET /v2/stats HTTP/1.1

to:

GET /v1/stats HTTP/1.1

7. Next, I decided to check if there were any interesting endpoints, so I performed a scan using the Jason Haddix tool that PawPawHacks/Tom Fieber edited to make even better, you can learn about it below in his video:

PawPawHacks/Tom Fieber Bookmarklet Update:
https://www.youtube.com/watch?v=gqg0kb4nQOU&t=279s
https://gist.github.com/tomfieber/9c3da63ab39d0017e7fed752be6d2330

Jason Haddix EndPoints Bookmarklet:
https://x.com/Jhaddix/status/1804225758795305365
https://gist.github.com/jhaddix/daba27d11fdd97d9077d610dccbe91df
https://github.com/jhaddix/pentest-bookmarks/blob/master/wiki/BookmarksList.wiki#user-content-Exploitation_Intro

8. Using the Jason Haddix tool, I found some interesting references to admin endpoints:
/static/js/main.99173f1b.js
/static/css/main.a4c2af1d.css
/
//
/dashboard
/start
/stats
/admin
/v2/login
/register
/v2/register
/login
/v2/stats
/v2/session/start
/v2/session/submit
/v2/session/history?limit=10
/v2/stats/leaderboard
/v2/admin/users
/v2/admin/sessions
/v2/admin/flag
/v2/verify-token

9. Next, in the "Request" pane for "GET /v2/stats", still in the "Replay" tab, I copied the Authorization Token and pasted it into CyberChef to decode it using the "JWT Decode" Recipe: https://gchq.github.io/CyberChef.  You can also use: https://jwtauditor.com.

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwidXNlcm5hbWUiOiJUZXN0ZXIxIiwicm9sZSI6InVzZXIiLCJpYXQiOjE3Njg1MjA1MDl9.LH_54bCfGwxDMRIMpsVqVfKNNAM0rokbpJ_UY3h3Pcs

Decoded to:

{
    "id": 4,
    "username": "Tester1",
    "role": "user",
    "iat": 1768520509
}

10. Next, I copied my decoded snippet, opened another instance of CyberChef, pasted it into the "Input" pane, and selected the "JWT Sign" Recipe.

11. Then, I changed the "id" to 1 and the "role" to "admin":

{
    "id": 1,
    "username": "Tester1",
    "role": "admin",
    "iat": 1768520509
}

12. Now, I copied to result of that newly encoded snippet and went back over to my Caido "Replay" tab and pasted that in, swapping out the existing Authorization Token with my newly created one: 

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwidXNlcm5hbWUiOiJUZXN0ZXIxIiwicm9sZSI6ImFkbWluIiwiaWF0IjoxNzY4NTIwNTA5fQ.HwzftLkURysyFN7JHrlQzExz5aHy4r8I5rNWyImBzHs

13. Next, still in the "Replay" tab, I changed the first line as below, and hit the red "Send" button and got the flag!!!

GET /v2/stats HTTP/1.1

to:

GET /v1/admin/flag HTTP/1.1

{
    "flag": "bug{0xePBUv175SMnexNCfymygGHwCoUEIqi}"
}


{
    "flag": "bug{sDlzhtTHMufXOT7QpGQPaumfWjQRDPMI}"
}

---)
