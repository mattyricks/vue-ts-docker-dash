<template>
  <div class="table-responsive">
    <table class="table table-sm">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col">Total</th>
          <th scope="col">Action</th>
        </tr>
      </thead>

      <tbody>
        <template v-for="order in orders" :key="order['id']">
          <tr>
            <td>
              {{ order["id"] }}
            </td>

            <td>
              {{ order["name"] }}
            </td>

            <td>
              {{ order["email"] }}
            </td>

            <td>
              {{ order["total"] }}
            </td>
          </tr>

          <tr>
            <td colspan="5">
              <div>
                <table class="table table-sm">
                  <thead>
                    <tr>
                      <th scope="col">#</th>
                      <th scope="col">Product Title</th>
                      <th scope="col">Quantity</th>
                      <th scope="col">Price</th>
                    </tr>
                  </thead>

                  <tbody>
                    <tr v-for="item in order['order_items']" :key="item.id">
                      <td>{item.id}</td>

                      <td>{item.product_title}</td>

                      <td>item.quantity</td>

                      <td>{item.price}</td>

                      <td>
                        <div class="btn-group mr-2">
                          <router-link
                            :to="`/products/${order['id']}/edit`"
                            class="btn btn-sm btn-outline btn-secondary"
                            >Edit</router-link
                          >

                          <a
                            href="javascript:void(0)"
                            class="btn btn-sm btn-outline btn-secondary"
                            >View</a
                          >
                        </div>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </td>
          </tr>
        </template>
      </tbody>
    </table>
  </div>

  <Paginator :last-page="lastPage" @page-changed="load($event)" />
</template>

<script lang="ts">
import { ref, onMounted } from "vue";
import axios from "axios";
import Paginator from "@/components/Paginator.vue";

export default {
  name: "OrdersVue",
  components: { Paginator },
  setup() {
    const orders = ref([]);
    const lastPage = ref(0);

    const load = async (page = 1) => {
      const { data } = await axios.get(`orders?page=${page}`);

      orders.value = data.data;
      lastPage.value = data.meta.last_page;
    };

    onMounted(load);

    return {
      orders,
      load,
    };
  },
};
</script>
