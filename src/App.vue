<template>
  <router-view v-if="userGoogle !== false" />
</template>

<script setup>
import { provide, ref } from "vue";
import { onAuthStateChanged } from "firebase/auth";
import { auth } from "./firebase";
import { useQuasar } from "quasar";

const userGoogle = ref(false);

provide("userGoogle", userGoogle);

const $q = useQuasar();

onAuthStateChanged(auth, (user) => {
  userGoogle.value = user;
  setTimeout(() => {
    $q.loading.hide();
  }, 30);
});

$q.loading.show();

</script>
