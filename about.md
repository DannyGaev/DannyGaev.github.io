---
layout: post
title: About
---

<div id="changes"></div>

You may have caught that em-dash, you'll be seeing more of them. I know it's pretentious, but I just can't let
<select name="options">
    <option value="1">Claude</option>
    <option value="2">Grok</option>
    <option value="3">ChatGPT</option>
    <option value="4">Gemini</option>
</select>
take that away from me.

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
    <td>IP Address</td>
    <td id="ipaddr"></td>
  </tr>
  <tr>
    <td>Rough Location</td>
    <td id="location"></td>
  </tr>
  <tr>
      <td>Less Rough Location</td>
      <td id="llocation"></td>
  </tr>
  <tr>
    <td>Browser Language</td>
    <td id="lang"></td>
  </tr>
  <tr>
    <td>Browser Platform</td>
    <td id="plat"></td>
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

    function setAttrs() {
        var ip = document.getElementById("ipaddr");
        var location = document.getElementById("location");
        var llocation = document.getElementById("llocation");
        var lang = document.getElementById("lang");
        var plat = document.getElementById("plat");

        lang.innerHTML = navigator.language;
        plat.innerHTML = navigator.platform;
        fetch("http://ip-api.com/json/").then(function (response) {
            return response.json();
        }).then(function (data) {
            ip.innerHTML = data.query;
            fetch(`https://api.hackertarget.com/geoip/?q=${data.query}&output=json`).then(function (response) {
                return response.json();
            }).then(function (data) {
                location.innerHTML = `${data.city}, ${data.state}, ${data.country}`
                llocation.innerHTML = `${data.latitude}, ${data.longitude}`
            }).catch(function (err) {
                location.innerHTML = "also unable to determine rough location";
                llocation.innerHTML = "you get the gist of it";
            });
        }).catch(function (err) {
            ip.innerHTML = "Unable to fetch IP Address";
        });
    }

    document.addEventListener('DOMContentLoaded', (event) => {
        checkCookie();
        setAttrs();
    });

</script>