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
import { useRouter } from "vue-router";

export default {
  name: "WrapperView",
  components: { NavBar, SideBar },
  setup() {
    const router = useRouter();

    onMounted(async () => {
      try {
        const { data } = await axios.get("user");

        console.log(data);
      } catch (error) {
        await router.push("/login");
      }
    });
  },
};
</script>

<style lang="scss" scoped>
</style>