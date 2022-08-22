<template>
  <NavBar />

  <div class="container-fluid">
    <div class="row">
      <SideBar />

      <main class="col-md-9 ms-sm-auto col-lg-10 px-md-4">
        <router-view />
      </main>
    </div>
  </div>
</template>

<script lang="ts">
import NavBar from "@/components/NavBar.vue";
import SideBar from "@/components/SideBar.vue";
import axios from "axios";
import { onMounted } from "vue";

export default {
  name: "WrapperView",
  components: { NavBar, SideBar },
  setup() {
    onMounted(async () => {
      const { data } = await axios.get("user");

      console.log(data);
    });
  },
};
</script>

<style lang="scss" scoped>
</style>