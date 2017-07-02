# **Drum-Kit**

This is part of the JavaScript30 movement, where we code and create a vanillaJS based project every day for 30 days. Today is day1 and I managed to finish the Drum Kit project, whose screenshot is beneath.

![alt](https://github.com/itaouil95/Drum-Kit/blob/master/drum-kit.png)

**Development**

So the project as briefly introduced before consisted in created a drum kit using just pure JavaScript. Where the user, helped by the GUI, which is showing the combination of sound to keyboard's key pressed can press one of the showed keys, and the event would fire a visual change as well as an audio playing. Like a Drum kit, yeahhhh.

How is this possible ? We start by actually creating the skeleton in HTML, by adding our keys and audio elements, each one of them, paired with a data-key attribute. Like the following:

```HTML
<div data-key="65" class="key">
  <kbd>A</kbd>
  <span class="sound">Clap</span>
</div>
```

We style our key elements and we add a transition effect. That is it for CSS.

Now let's move to the vanillaJS part. The first step towards the accomplishment of the task is to set an event listener on key down, select the audio element play the audio element with the same keycode as the event. Second, we select the key with the same data-key as the keycode of the event and we apply our transitioning class. This all it has to happens in our window event. The following snippet represents the steps described:

```JavaScript
<script>

  // Callback function
  function playSound(e) {

    // Select audio tag with same data-key as e.keyCode
    const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);

    // Select div tag with same data-key as e.keyCode
    const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);

    // Skip function if audio is NULL
    if (!audio) return;

    // Otherwise play audio with rewind
    audio.currentTime = 0;
    audio.play();

    // Add transform effect to selected key
    key.classList.add("playing");

  }

  // Add event listener
  window.addEventListener("keydown", playSound);

</script>
```

Now we have our effect when we press the key, and the sound plays continuously as you would expect from a good drum kit. However, we need to find a way to select the selected key and remove the transitioning effect when the transition ends. To accomplish this we need to add a transitionend event listener on all keys and act upon it. Let's see how this is done:

```JavaScript
<script>

  // Callback function
  function transitionEnd(e) {

    // Skip if transform transition not done yet
    if (e.propertyName !== "transform") return;

    // Otherwise remover transition class
    // this refers to the calling element
    // in the function, aka key in this case
    this.classList.remove("playing");

  }

  // Select all keys
  const keys = document.querySelectorAll(".keys");

  // Add event listener on node list
  keys.forEach(key => key.addEventListener("transitionend", transitionEnd));

</script>
```

There you go. Everything should be good now.

**N.B:** Check out wesbos.io for more info about the challenge ! Happy coding !.
