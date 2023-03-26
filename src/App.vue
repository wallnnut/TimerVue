<template>
  <div class="container">
    <div class="timers">
      <TimerDefault @resetTimer="resetTimer" v-bind:timer="t" v-for="(t) in timers" :key="t"/>
      <AddButton @add-timer="addTimer" />
    </div>
  </div>
</template>

<script>
import AddButton from "./components/AddButton.vue";
import TimerDefault from "./components/TimerDefault.vue";

export default {
  name: "App",
  components: {
    AddButton,
    TimerDefault,
  },
  data() {
    return {
      timers: [],
    };
  },
  methods: {
    addTimer() {
      this.timers.push({
        id: Math.floor((1 + Math.random()) * 0x10000).toString(16).substring(1),
        isActive: false,
        isStoped: false,
        hours: 0,
        minutes: 0,
        seconds: 0,
        interval: null,
      });
    },
    resetTimer(id) {
      this.timers = this.timers.map((timer) => {
        if (timer.id === id) {
          return {
            ...timer,
            isActive: false,
            isStoped: false,
            hours: 0,
            minutes: 0,
            seconds: 0,
            interval: null,
          };
        } return timer;
      });
    },
  },
};
</script>

<style lang="scss">
* {
padding: 0;
margin: 0;
border: 0;
}

*,
*:before,
*:after {
-moz-box-sizing: border-box;
-webkit-box-sizing: border-box;
box-sizing: border-box;
}
:focus,
:active {
outline: none;
}
a:focus,
a:active {
outline: none;
}
nav,
footer,
header,
aside {
display: block;
}

html,
body {
height: 100%;
width: 100%;
font-size: 100%;
line-height: 1;
font-size: 14px;
-ms-text-size-adjust: 100%;
-moz-text-size-adjust: 100%;
-webkit-text-size-adjust: 100%;
}

input,
button,
textarea {
font-family: inherit;
}

input::-ms-clear {
display: none;
}
button {
cursor: pointer;
}
button::-moz-focus-inner {
padding: 0;
border: 0;
}
a,
a:visited {
text-decoration: none;
}
a:hover {
text-decoration: none;
}
ul,
li {
list-style: none;
}
img {
vertical-align: top;
}

h1,
h2,
h3,
h4,
h5,
h6 {
font-weight: inherit;
}

.container {
margin: 0 auto;
max-width: 1200px;
padding: 5px 10px;
min-height: 100vh;
display: flex;
flex-direction: column;
align-items: center;
}

.timers {
  margin-top: 72px;
  align-items: center;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 50px;
  justify-content: center;
}
@media (max-width: 800px) {
  .timers {
  grid-template-columns: repeat(2, 1fr);
  }
}
@media (max-width: 520px) {
  .timers {
  grid-template-columns: 1fr;
  }
}
#app {
  background-color:  #353638;;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #9E9E9E;
  height: 100vh;
  overflow: auto;
}
</style>
