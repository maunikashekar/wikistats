<script>
import AppBar from "./components/AppBar.vue";
import Table from "./components/Table.vue";
import Stats from "./components/Stats.vue";
import Images from "./components/Images.vue";
export default {
  name: "App",
  provide() {
    return {
      appName: "WikiStats",
      username: "Maunika Shekar",
      tagline: "Powered by English Wikipedia",
    };
  },
  components: {
    AppBar,
    Table,
    Stats,
    Images,
  },
};
</script>

<template>
  <AppBar />
  <div class="bodyPanel">
    <Table />
    <Stats />
    <Images />
  </div>
</template>

<style scoped>
.bodyPanel {
  width: 100%;
  display: flex;
  flex-direction: row;
}
</style>
