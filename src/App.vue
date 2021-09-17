<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <br />
    {{ message }}
    <HelloWorld msg="Здесь могла быть ваша реклама" :isShow="show" />
    <input
      type="text"
      placeholder="text"
      @keydown="blurMethod"
      @keyup="focusMethod"
      @blur="blurMethod"
      @focus="focusMethod"
    />
    <!-- @click or v-on:click -->
    <button @click="c = a + b">Click</button>
    <button @click="doThat('Hello', $event)">Click</button>
    {{ c }}
    <calc />
  </div>
</template>

<script>
import Calc from "./components/Calc.vue";
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    Calc,
  },
  data: () => ({
    message: "Привет, Vue",
    show: false,
    c: 0,
    a: 1,
    b: 1,
  }),
  methods: {
    doThat(str, event) {
      console.log(str, event);
      this.c = 0;
    },
    blurMethod() {
      console.log("blure");
    },
    focusMethod() {
      console.log("focus");
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
