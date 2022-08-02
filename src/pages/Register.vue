<template>
  <main class="form-signin w-100 m-auto">
    <form @submit.prevent="submit">
      <h1 class="h3 mb-3 fw-normal">Please Register Here</h1>

      <input
        v-model="firstName"
        class="form-control"
        placeholder="First Name"
        required
      />

      <input
        v-model="lastName"
        class="form-control"
        placeholder="Last Name"
        required
      />

      <input
        v-model="email"
        type="email"
        class="form-control"
        placeholder="Email"
        required
      />

      <input
        v-model="password"
        type="password"
        class="form-control"
        placeholder="Password"
        required
      />

      <input
        v-model="passwordConfirm"
        type="password"
        class="form-control"
        placeholder="Confirm Password"
        required
      />

      <button class="w-100 btn btn-lg btn-primary" type="submit">Submit</button>
    </form>
  </main>
</template>

<script lang="ts">
import { ref } from "vue";

export default {
  name: "RegisterComponent",
  setup() {
    const firstName = ref("");
    const lastName = ref("");
    const email = ref("");
    const password = ref("");
    const passwordConfirm = ref("");

    const submit = () => {
      console.log({
        first_name: firstName.value,
        last_name: lastName.value,
        email: email.value,
        password: password.value,
        passwordConfirm: passwordConfirm.value,
      });
    };

    //     const firstName = ref(value: '')
    // const lastName = ref(value: '')
    // const email = ref(value: '')
    // const password = ref(value: '')
    // const passwordConfirm = ref(value: '')

    return {
      firstName,
      lastName,
      email,
      password,
      passwordConfirm,
      submit,
    };
  },
};
</script>

<style scoped>
html,
body {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  padding-top: 40px;
  padding-bottom: 40px;
  background-color: #f5f5f5;
}

.form-signin {
  max-width: 330px;
  padding: 15px;
}

.form-signin .form-floating:focus-within {
  z-index: 2;
}

.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}

.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>
