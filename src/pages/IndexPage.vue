<template>
  <q-page class="flex flex-center">
    <div class="row text-center">
      <div class="col-12 text-h6 text-weight-bold">
        Курс валют на {{ currentDate.format("D MMMM YYYY") }} 💸
      </div>
      <div class="col-12 text-h8">💲 1 USD = {{ currentVal }}RUB 🪆</div>
    </div>
  </q-page>
</template>

<script setup>
import { api } from "src/boot/axios";
import { ref } from "vue";
import dayjs from "dayjs";

import { useQuasar } from "quasar";

const $q = useQuasar();
const currentDate = ref(dayjs());
const currentVal = ref(0);

window.addEventListener("offline", (event) => {
  $q.notify({
    color: "accent",
    message: "Нет сети",
    multiLine: true,
    position: "bottom",
  });
});

window.addEventListener("online", (event) => {
  $q.notify({
    color: "positive",
    message: "Подключено",
    multiLine: true,
    position: "bottom",
  });
});

api.get("https://www.cbr-xml-daily.ru/daily_json.js").then((response) => {
  currentVal.value = response.data.Valute.USD.Value;
  console.log(currentVal.value);
});
</script>
