---
layout: post
title: About
---

<div id="changes"></div>
<br>

You may have caught that em-dash, you'll be seeing more of them. I know it's pretentious, but I cannot let
<select name="options">
    <option value="1">Claude</option>
    <option value="2">Grok</option>
    <option value="3">ChatGPT</option>
    <option value="4">Gemini</option>
</select>
take that away from me.

<br>
<br>
My name is Daniel Gaevskiy (shortened here to Gaev for ease of pronunciation). I am a Computer Science-turned-Cybersecurity student, 
soon to have graduated from university. On this website you can find some of the <a href="https://dannygaev.com/projects/">Projects</a> I've completed, Capture The Flag (CTF) challenges
I've solved and felt proud enough to <a href="https://dannygaev.com/writeups/">Write-Up</a>, and a look at the <a href="https://dannygaev.com/competitions/">Competitions</a> I've completed and how I approach them.

Pages will change depending on when you visit them, but all the code behind that is running client side for two noble reasons:
<ol>
  <li>There will be no server-side delinquency or sleight-of-byte, and</li>
  <li>This site runs off of GitHub Pages.</li>
</ol>
As such, everything you see is available for perusal in your browser -- for instance, here's the information that you as a visitor give to me when you open a website:

<table>
  <tr>
    <th>Attribute</th>
    <th>Value</th>
  </tr>
  <tr>
    <td>Alfreds Futterkiste</td>
    <td>Maria Anders</td>
  </tr>
  <tr>
    <td>Centro comercial Moctezuma</td>
    <td>Francisco Chang</td>
  </tr>
  <tr>
    <td>Ernst Handel</td>
    <td>Roland Mendel</td>
  </tr>
  <tr>
    <td>Island Trading</td>
    <td>Helen Bennett</td>
  </tr>
  <tr>
    <td>Laughing Bacchus Winecellars</td>
    <td>Yoshi Tannamuri</td>
  </tr>
  <tr>
    <td>Magazzini Alimentari Riuniti</td>
    <td>Giovanni Rovelli</td>
  </tr>
</table>

<script>
    function getCookie(cname) {
            let name = cname + "=";
            let decodedCookie = decodeURIComponent(document.cookie);
            let ca = decodedCookie.split(';');
            for (let i = 0; i < ca.length; i++) {
                let c = ca[i];
                while (c.charAt(0) == ' ') {
                    c = c.substring(1);
                }
                if (c.indexOf(name) == 0) {
                    return c.substring(name.length, c.length);
                }
            }
            return "";
        }

    function checkCookie() {
        var title = document.getElementsByClassName("post-title");
        var div_changes = document.getElementById("changes");
        let reoffender = getCookie("reoffender");
        if (reoffender != "") {
            title[0].innerHTML = "Welcome back!";
            div_changes.innerHTML = "It's nice to see you again -- feel free to skip the rest here, it's the same as last time."
        }
        else {
            document.cookie = "reoffender=true";
            title[0].innerHTML = "Hello There!";
            div_changes.innerHTML = "I've noticed it's your first time here -- welcome!"

        }
    }
    document.addEventListener('DOMContentLoaded', (event) => {
        checkCookie();
    });

</script>