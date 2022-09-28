<template>
  <div class="table-responsive">
    <table class="table table-striped table-sm">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Image</th>
          <th scope="col">Title</th>
          <th scope="col">Description</th>
          <th scope="col">Price</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="product in products" :key="product['id']">
          <td>{{ product["id"] }}</td>
          <td>
            <img :src="product['image']" width="50" alt="" />
          </td>

          <td>{{ product["title"] }}</td>
          <td>{{ product["description"] }}</td>
          <td>{{ product["price"] }}</td>
          <td>
            <div class="btn-group mr-2">
              <router-link
                :to="`/products/${product['id']}/edit`"
                class="btn btn-sm btn-outline btn-secondary"
                >Edit</router-link
              >

              <a
                href="javascript:void(0)"
                class="btn btn-sm btn-outline btn-secondary"
                @click="del(product['id'])"
                >Delete</a
              >
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>

  <nav>
    <ul class="pagination">
      <li class="page-item">
        <a href="javascript:void(0)" class="page-link" @click="prev"
          >Previous</a
        >
      </li>

      <li class="page-item">
        <a href="javascript:void(0)" class="page-link" @click="next">Next</a>
      </li>
    </ul>
  </nav>
</template>

<script lang="ts">
import { onMounted, ref, watch } from "vue";
import axios from "axios";
import { Product } from "@/models/product";

export default {
  name: "ProductsComponent",
  setup() {
    const products = ref([]);
    const page = ref(1);
    const lastPage = ref(0);

    const load = async () => {
      const { data } = await axios.get(`products?page=${page.value}`);

      products.value = data.data;
      lastPage.value = data.meta.last_page;
    };

    onMounted(load);

    watch(page, load);

    const next = async () => {
      if (page.value < lastPage.value) {
        page.value++;
      }
    };

    const prev = async () => {
      if (page.value > 1) {
        page.value--;
      }
    };

    const del = async (id: number) => {
      if (confirm("Are you sure?")) {
        await axios.delete(`products/${id}`);
      }

      products.value = products.value.filter((p: Product) => p.id !== id);
    };

    return {
      products,
      del,
      next,
      prev,
    };
  },
};
</script>
