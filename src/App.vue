<template>
  <div id="app">
    <menus />
    <div @click="handleClick('Out')" class="image-container">
      <img
        @click="handleClick('In')"
        src="https://vuejs.org/images/icons/favicon-32x32.png"
        class="image"
      />
    </div>
    <h1 style="user-select: none; cursor: default;">{{ msgIn }}</h1>
    <h1 style="user-select: none; cursor: default;">{{ msgOut }}</h1>
  </div>
</template>

<script>
import starlette from "starlette";
import menus from "./components/menus";

export default {
  name: "app",
  data: () => ({
    csInterface: null,
    clickIn: 0,
    clickOut: 0
  }),
  components: {
    menus
  },
  computed: {
    msgIn() {
      return this.clickIn
        ? `Clicked ${this.clickIn} time${this.clickIn > 1 ? "s" : ""}`
        : "No clicks";
    },
    msgOut() {
      return this.clickOut
        ? `Clicked ${this.clickOut} time${this.clickOut > 1 ? "s" : ""}`
        : "No clicks";
    }
  },
  mounted() {
    console.clear();
    this.csInterface = new CSInterface();
    starlette.init();

    document.body.addEventListener("click", e => {
      console.log(e.timeStamp);
    });
  },
  methods: {
    handleClick(type) {
      return this[`click${type}`]++;
    }
  }
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  text-align: center;
  margin-top: 60px;
}

.image {
  background-color: var(--color-btn-hover);
}

.image-container {
  cursor: pointer;
  background-color: var(--color-scrollbar);
  display: flex;
  padding: 10px;
  justify-content: center;
  align-items: center;
}

/* Various helper styles to match application theme */
@import url("https://fonts.googleapis.com/css?family=Open+Sans&display=swap");
:root {
  --quad: cubic-bezier(0.48, 0.04, 0.52, 0.96);
  --quart: cubic-bezier(0.76, 0, 0.24, 1);
  --quint: cubic-bezier(0.84, 0, 0.16, 1);

  background-color: var(--color-bg);
  color: var(--color-default);
  font-family: "Open Sans", sans-serif;
  font-size: 10px;
  height: 100vh;
  width: 100vw;
}

#app::-webkit-scrollbar {
  display: block;
}
body::-webkit-scrollbar {
  width: 0px;
}

::-webkit-scrollbar {
  background-color: var(--color-scrollbar);
  width: var(--width-scrollbar-track);
}
::-webkit-scrollbar-thumb {
  width: var(--width-scrollbar-track);
  background: var(--color-scrollbar-thumb);
  border-radius: var(--radius-scrollbar-thumb);
}
::-webkit-scrollbar-thumb:hover {
  background: var(--color-scrollbar-thumb-hover);
}
::-webkit-scrollbar-resizer {
  display: none;
  width: 0px;
  background-color: transparent;
}
::-webkit-scrollbar-button {
  height: 0px;
}
::-webkit-scrollbar-corner {
  display: none;
}
</style>
