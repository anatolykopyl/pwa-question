# pwa-test

[Original Stack Overflow question](https://stackoverflow.com/questions/68716680/accessing-css-variable-on-mount-in-vue)

I'm working on a Vue.js PWA that requires the js to know the value of `env(safe-area-inset-top)`. I have the `env` reassigned to a css variable named `--sat` which I'm reading. But I can't find a way to get its value at the beginning of the lifecycle.

The [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/API/Window/load_event) says that 
>The Window `load` event is fired when the whole page has loaded, including all dependent resources such as **stylesheets** and images.

So i've tried the following:
```javascript
methods: {
  setSat() {
    this.sat = getComputedStyle(document.body).getPropertyValue('--sat');
  },
},
mounted() {
  window.onload = this.setSat;
},
```
However this doesn't seem to work. When I open the project on my phone from the home screen as a PWA the `setSat` method does get called by itself but returns `0px`. If I trigger it by clicking a button after the page is loaded it returns the appropriate `48px`.

If I try to run the function on a 0 or even 100ms timeout, the value of `env(safe-area-inset-top)` is still `0px`.

For now I've resorted to waiting a second before getting the value but this is obviously not desirable.
