---
layout: post
title: Pair Programming (Cookie Clicker) - Neil C
type: issues
description: This is a Cookie Clicker that was made for the Pair Programming Project. I collaborated with my peer and asked them for feedback on this code.
comments: true
---

<div>
    <h3> Cookie Clicker </h3>
    <p> Click the cookie as many times as possible, you can see your score on the left of the cookie. Have fun. </p>
    <p> Keep in mind that the cookie counter resets once you leave or reload the page</p>
</div>

<style>
    .cookiepicture {
        background-color: transparent;
    }
</style>

<!--<button class="cookiepicture" type="submit">-->
<img src="../../../images/cookie.png" alt="cookiepic" id="cookiepicture" width="450" height="250"/>
<!--</button>-->

<p>
    Cookie Clicked <span id="display">0</span> Times
</p>
<script type="text/javascript">
    let count = 0;
    let cookiepicture = document.getElementById("cookiepicture");
    let disp = document.getElementById("display");
         
    cookiepicture.onclick = function () {
                count++;
    disp.innerHTML = count;
    }
</script>