<template>
  <form @submit.prevent="submit">
    <div class="mb-3">
      <label>Title</label>
      <input v-model="data.title" name="title" class="form-control" />
    </div>

    <div class="mb-3">
      <label>Description</label>
      <input
        v-model="data.description"
        name="description"
        class="form-control"
      />
    </div>

    <div class="mb-3">
      <label>Image</label>
      <div class="input-group">
        <input v-model="data.image" name="image" class="form-control" />

        <ImageUpload @uploaded="data.image = $event" />
      </div>
    </div>

    <div class="mb-3">
      <label>Price</label>
      <input
        v-model="data.price"
        type="number"
        name="price"
        class="form-control"
      />
    </div>

    <button class="btn btn-outline-secondary">Save</button>
  </form>
</template>

<script lang="ts">
import { reactive } from "vue";
import axios from "axios";
import { useRouter } from "vue-router";
import ImageUpload from "@/components/ImageUpload.vue";

export default {
  name: "ProductCreate",
  components: { ImageUpload },
  setup() {
    const router = useRouter();
    const data = reactive({
      title: "",
      description: "",
      image: "",
      price: "",
    });
    const submit = async () => {
      await axios.post("products", data);
      await router.push("/products");
    };
    return {
      data,
      submit,
    };
  },
};
</script>
