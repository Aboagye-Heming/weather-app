<template>
  <div class="app">
   heming
  </div>
</template>

<script>
export default (await import("vue")).defineComponent({
  name: "weatherApp",
  components: {},
  data() {
    return {};
  },
  methods: {},
});
</script>

<style>
body {
  background-color: #121212;
}
.header {
  background-color: #212730;
  border-radius: 20px;
  color: #fff;
  text-align: center;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  margin-top: 5rem;
}
.btn-search {
  background-image: linear-gradient(to left, cyan, magenta);
}
</style>
