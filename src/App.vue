<template>
  <div>
    <TheHeader :title1="headerTtitle[0]" :title2="headerTtitle[1]" />
    <TheTable />
  </div>
</template>

<script>
import { reactive } from "vue";
import TheHeader from "./components/TheHeader.vue";
import TheTable from "./components/TheTable.vue";

export default {
  components: { TheHeader, TheTable },
  setup() {
    const headerTtitle = reactive(["Home", "Desk"]);

    return { headerTtitle };
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

a {
  color: inherit;
  text-decoration: none;
}
</style>
