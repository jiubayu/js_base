<template>
    app
    <clipboard />
    <keyboard/>
    <ShortURL />
    <ScreenShot/> 
</template> 
<script>
import Clipboard from './components/Clipboard.vue';
import Keyboard from './components/Keyboard.vue';
import ShortURL from './components/ShortURL.vue';
import ScreenShot from './components/WebRTCScreenShot.vue';
export default {
  name: 'App',
  components: {
    Clipboard,
    Keyboard,
    ShortURL,
    ScreenShot
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
