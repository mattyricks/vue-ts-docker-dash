<template>
  <form @submit.prevent="submit">
    <div class="mb-3">
      <label for="">First Name</label>
      <input v-model="data.first_name" name="first_name" class="form-control" />
    </div>

    <div class="mb-3">
      <label for="">Last Name</label>
      <input v-model="data.last_name" name="last_name" class="form-control" />
    </div>

    <div class="mb-3">
      <label for="">Email</label>
      <input v-model="data.email" name="email" class="form-control" />
    </div>

    <div class="mb-3">
      <label for="">Role</label>
      <select v-model="data.role_id" name="role_id" class="form-control">
        <option v-for="role of roles" :key="role['id']" :value="role['id']">
          {{ role["name"] }}
        </option>
      </select>
    </div>

    <button class="btn btn-outline-secondary">Save</button>
  </form>
</template>

<script lang="ts">
import { reactive, ref, onMounted } from "vue";
import axios from "axios";
import { useRouter } from "vue-router";

export default {
  name: "UserCreate",
  setup() {
    const data = reactive({
      first_name: "",
      last_name: "",
      email: "",
      role_id: "",
    });

    const roles = ref([]);
    const router = useRouter();

    onMounted(async () => {
      const { data } = await axios.get("roles");
      roles.value = data;
    });

    const submit = async () => {
      await axios.post("users", data);
      await router.push("/users");
    };

    return {
      data,
      roles,
      submit,
    };
  },
};
</script>

<style lang="scss" scoped>
</style>