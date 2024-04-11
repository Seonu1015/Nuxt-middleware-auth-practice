<script setup lang="ts">
import { ref } from "vue";

definePageMeta({
  layout: "login",
});

const loginInfo = ref({
  form: false,
  id: "",
  password: "",
  loading: false,
}).value;

const { currentUser, login } = useAuth();

const onSubmit = async () => {
  if (!loginInfo.form) return;

  loginInfo.loading = true;
  console.log("id : " + loginInfo.id + ", password : " + loginInfo.password);

  setTimeout(() => (loginInfo.loading = false), 2000);

  await login();
};

const required = (v: any) => !!v || "Field is required";
</script>

<template>
  <v-sheet class="pa-12" rounded>
    <v-card class="mx-auto px-6 py-8" max-width="344">
      <v-form v-model="loginInfo.form" @submit.prevent="onSubmit">
        <v-text-field
          v-model="loginInfo.id"
          :readonly="loginInfo.loading"
          :rules="[required]"
          class="mb-2"
          label="아이디"
          variant="solo"
          clearable
        ></v-text-field>

        <v-text-field
          v-model="loginInfo.password"
          :readonly="loginInfo.loading"
          :rules="[required]"
          label="비밀번호"
          type="password"
          variant="solo"
          clearable
        ></v-text-field>

        <br />

        <v-btn
          :disabled="!loginInfo.form"
          :loading="loginInfo.loading"
          color="light-blue-darken-3"
          size="large"
          type="submit"
          variant="elevated"
          block
        >
          Sign In
        </v-btn>
      </v-form>
    </v-card>
  </v-sheet>
</template>
