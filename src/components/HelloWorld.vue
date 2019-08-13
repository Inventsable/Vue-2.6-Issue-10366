<template>
  <div></div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  computed: {
    // Use as this.app
    app() {
      return this.$root.$children[0];
    },
    // Use as this.cs
    cs() {
      return this.app.csInterface;
    }
  },
  mounted() {
    console.log("Top-level root instance (App.vue):");
    console.log(this.app);
    console.log("CSInteface:");
    console.log(this.cs);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
</style>
