<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title> Vostrikov Currency {{ platform }}</q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { computed } from "vue";
import { useQuasar } from "quasar";
const $q = useQuasar();

const platform = computed(() => {
  return $q.platform.is.capacitor ? "(mobile)" : "";
});
</script>
