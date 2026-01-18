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



<details markdown>
  <br>
    <summary>[Password Cracking - FCrackZip (Credit to <a href="https://www.linkedin.com/in/tawon-saetang">Tawon Saetang</a> for introducing me to this tool!]</summary>
<ul class="c8 lst-kix_list_37-0"><li class="c0 li-bullet-0"><span class="c9">Fcrackzip</span></li></ul><p class="c4"><span class="c2">If you don&rsquo;t use the &ndash;u switch, FCrackZip will give you a list of possible passwords, but if you use &ndash;u, it&rsquo;s my understanding that the &ndash;u stands for &ldquo;unzip&rdquo; and it takes longer, but if used, will first try to unzip the encrypted file using the possible passwords, and only give you the actual password, if it finds it, instead of a list of possible passwords.</span></p><p class="c3"><span class="c2"></span></p><p class="c4"><span class="c2">See the two examples compared below, the first example does not use the -u switch:</span></p><p class="c3"><span class="c2"></span></p><p class="c4"><span class="c2">&#9484;&#9472;&#9472;(root&#12927;kali)-[/home/kali/Desktop/ToCrack]</span></p><p class="c4"><span class="c2">&#9492;&#9472;# fcrackzip -b --method 2 -D -p /usr/share/john/rockyou.txt /home/kali/Desktop/ToCrack/test.zip</span></p><p class="c3"><span class="c1"></span></p><p class="c4"><span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 713.13px; height: 208.00px;"><img alt="" src="images/image142.png" style="width: 713.13px; height: 208.00px; margin-left: 0.00px; margin-top: 0.00px; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px);" title=""></span></p><p class="c4"><span class="c2">And the following example does use the -u switch, see the difference?</span></p><p class="c4"><span class="c2">&#9484;&#9472;&#9472;(root&#12927;kali)-[/home/kali/Desktop/ToCrack]</span></p><p class="c4"><span class="c2">&#9492;&#9472;# fcrackzip -u -D -p /usr/share/john/rockyou.txt /home/kali/Desktop/ToCrack/f0007474_ore.zip</span></p><p class="c3"><span class="c2"></span></p><p class="c4"><span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 708.00px; height: 138.60px;"><img alt="" src="images/image144.png" style="width: 708.00px; height: 138.60px; margin-left: 0.00px; margin-top: 0.00px; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px);" title=""></span></p><ul class="c8 lst-kix_list_42-0 start"><li class="c0 li-bullet-0"><span class="c11"><a class="c6" href="https://www.google.com/url?q=https://www.youtube.com/watch?v%3D7f2130_MuZE%26ab_channel%3DMotasemHamdan&amp;sa=D&amp;source=editors&amp;ust=1699590511423827&amp;usg=AOvVaw1nCbkOP8tvOd9SC5YDKk9-">https://www.youtube.com/watch?v=7f2130_MuZE&amp;ab_channel=MotasemHamdan</a></span></li><li class="c0 li-bullet-0"><span class="c2">(5 1/2 minutes in): &nbsp;</span><span class="c11"><a class="c6" href="https://www.google.com/url?q=https://www.youtube.com/watch?v%3D7f2130_MuZE&amp;sa=D&amp;source=editors&amp;ust=1699590511424343&amp;usg=AOvVaw3IC5Zf3A1JaZblwpyhreVK">https://www.youtube.com/watch?v=7f2130_MuZE</a></span></li><li class="c0 li-bullet-0"><span class="c11"><a class="c6" href="https://www.google.com/url?q=https://www.youtube.com/watch?v%3D4IqarU1Q60s&amp;sa=D&amp;source=editors&amp;ust=1699590511424697&amp;usg=AOvVaw0fgH5Lq5At2T5wAik3K42q">https://www.youtube.com/watch?v=4IqarU1Q60s</a></span></li><li class="c0 li-bullet-0"><span class="c11"><a class="c6" href="https://www.google.com/url?q=https://www.kali.org/tools/fcrackzip&amp;sa=D&amp;source=editors&amp;ust=1699590511425042&amp;usg=AOvVaw3QK_IjJ9QSc6IQ0pzGFgtj">https://www.kali.org/tools/fcrackzip</a></span></li><li class="c0 li-bullet-0"><span class="c11"><a class="c6" href="https://www.google.com/url?q=https://github.com/foreni-packages/fcrackzip&amp;sa=D&amp;source=editors&amp;ust=1699590511425366&amp;usg=AOvVaw1aaAnn9-IZExlf3_ZpMBDI">https://github.com/foreni-packages/fcrackzip</a></span></li><li class="c0 li-bullet-0"><span class="c11"><a class="c6" href="https://www.google.com/url?q=http://oldhome.schmorp.de/marc/fcrackzip.html&amp;sa=D&amp;source=editors&amp;ust=1699590511425694&amp;usg=AOvVaw1NfOVPgqD-f60bOUN4bHAC">http://oldhome.schmorp.de/marc/fcrackzip.html</a></span></li><li class="c0 li-bullet-0"><span class="c11"><a class="c6" href="https://www.google.com/url?q=https://www.geeksforgeeks.org/fcrackzip-tool-crack-a-zip-file-password-in-kali-linux&amp;sa=D&amp;source=editors&amp;ust=1699590511426062&amp;usg=AOvVaw3AY4luncqXGMRVZMWFwynF">https://www.geeksforgeeks.org/fcrackzip-tool-crack-a-zip-file-password-in-kali-linux</a></span></li><li class="c0 li-bullet-0"><span class="c11"><a class="c6" href="https://www.google.com/url?q=https://manpages.ubuntu.com/manpages/trusty/man1/fcrackzip.1.html&amp;sa=D&amp;source=editors&amp;ust=1699590511426415&amp;usg=AOvVaw2bc0wuiLOfsETi4ILy7VvI">https://manpages.ubuntu.com/manpages/trusty/man1/fcrackzip.1.html</a></span></li><li class="c0 li-bullet-0"><span class="c11"><a class="c6" href="https://www.google.com/url?q=https://www.hackingarticles.in/comprehensive-guide-on-fcrackzip-tool&amp;sa=D&amp;source=editors&amp;ust=1699590511426755&amp;usg=AOvVaw03UxfZeRupDEMK2hyIruH0">https://www.hackingarticles.in/comprehensive-guide-on-fcrackzip-tool</a></span></li><li class="c0 li-bullet-0"><span class="c11"><a class="c6" href="https://www.google.com/url?q=https://infosecwriteups.com/beginners-ctf-guide-finding-hidden-data-in-images-e3be9e34ae0d&amp;sa=D&amp;source=editors&amp;ust=1699590511427132&amp;usg=AOvVaw34lbIrGwI9X_dSYiyw6Tb6">https://infosecwriteups.com/beginners-ctf-guide-finding-hidden-data-in-images-e3be9e34ae0d</a></span></li><li class="c0 li-bullet-0"><span class="c11"><a class="c6" href="https://www.google.com/url?q=https://www.tenorshare.com/windows-tips/how-to-remove-password-from-zip-file-without-any-software.html&amp;sa=D&amp;source=editors&amp;ust=1699590511427561&amp;usg=AOvVaw2h_zw11G14MEvMs0F0V3Go">https://www.tenorshare.com/windows-tips/how-to-remove-password-from-zip-file-without-any-software.html</a></span></li></ul>
</details>
 <br>


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
    "flag": "bug{}"
}


{
    "flag": "bug{}"
}

---)
