---
layout: post
title: React, analizando el código y estructura.
excerpt_separator: <!--more-->
---

<html>
<head>
  <style type="text/css">
    .key {
        border-style: solid;
        border-color: black;
        border-width: 0 1px 1px 1px;
        height: 6em;
        width: 3em;
        text-align: center;
        transition: all 0.07s; 
        display: inline-block;
        padding-top: 55px;
        margin: -2.5px;
        background-color: white;
    }

    .playing {
        transform: scale(0.95);
        box-shadow: 0 0 15px grey inset;
    }
  </style>
</head>
<body>
    <div id="keys">
        <div data-key="65" class="key">
            <kbd>A</kbd>
        </div>
        <div data-key="83" class="key">
            <kbd>S</kbd>
        </div>
        <div data-key="68" class="key">
            <kbd>D</kbd>
        </div>
        <div data-key="70" class="key">
            <kbd>F</kbd>
        </div>
        <div data-key="71" class="key">
            <kbd>G</kbd>
        </div>
        <div data-key="72" class="key">
            <kbd>H</kbd>
        </div>
        <div data-key="74" class="key">
            <kbd>J</kbd>
        </div>
        <div data-key="75" class="key">
            <kbd>K</kbd>
        </div>
    </div>

    <audio data-key="65" src="../sounds/do.wav"></audio>
    <audio data-key="83" src="../sounds/re.wav"></audio>
    <audio data-key="68" src="../sounds/mi.wav"></audio>
    <audio data-key="70" src="../sounds/fa.wav"></audio>
    <audio data-key="71" src="../sounds/sol.wav"></audio>
    <audio data-key="72" src="../sounds/la.wav"></audio>
    <audio data-key="74" src="../sounds/si.wav"></audio>
    <audio data-key="75" src="../sounds/do.wav"></audio>

    <script>
        window.addEventListener("load", function() {
            window.addEventListener('keydown', function (e) {
            const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
            const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);
            if(!audio) return;
            audio.currentTime = 0;
            audio.play();
            key.classList.add('playing');
        })

        function removeTransition(e) {
            if(e.propertyName !== 'transform') return;
            this.classList.remove("playing");
        }

        const key = document.querySelectorAll('.key')   ;
        key.forEach(key => key.addEventListener("transitionend", removeTransition));
    })
    </script>


</body>
</html>