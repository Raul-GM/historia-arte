<template>
  <ArtList />
</template>

<script>
import ArtList from './components/ArtList.vue'

export default {
  name: 'App',
  components: {
    ArtList
  }
}
</script>

<style>
:root {
  --main-color: #2c3e50;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--main-color);
  margin-top: 30px;
}

@font-face {
  font-family: 'icomoon';
  src:  url('./../src/assets/fonts/icomoon.eot?gbuck3');
  src:  url('./../src/assets/fonts/icomoon.eot?gbuck3#iefix') format('embedded-opentype'),
    url('./../src/assets/fonts/icomoon.ttf?gbuck3') format('truetype'),
    url('./../src/assets/fonts/icomoon.woff?gbuck3') format('woff'),
    url('./../src/assets/fonts/icomoon.svg?gbuck3#icomoon') format('svg');
  font-weight: normal;
  font-style: normal;
  font-display: block;
}

[class^="icon-"], [class*=" icon-"] {
  /* use !important to prevent issues with browser extensions that change fonts */
  font-family: 'icomoon' !important;
  speak: never;
  font-style: normal;
  font-weight: normal;
  font-variant: normal;
  text-transform: none;
  line-height: 1;

  /* Better Font Rendering =========== */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.icon-solve:before {
  content: "\e902";
}
.icon-flag:before {
  content: "\e900";
}
.icon-next:before {
  content: "\e901";
}
.icon-button {
  border: 2px solid var(--main-color);
  border-radius: 8px;
  padding: .5rem;
  font-size: 14px;
  margin: 0 1rem;
  cursor: pointer;
  transition: .3s all;
}
.icon-button:hover {
  color: #f1f1f1;
  background-color: var(--main-color);
}
</style>
