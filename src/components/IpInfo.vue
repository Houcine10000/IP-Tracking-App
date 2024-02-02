<template>
  <v-container
    style="position: absolute; top: 180px; min-width: 120%;"
    class="pa-0"
  >
    <v-row>
      <v-col cols="3" class="pa-0">
        <v-card elevation="0" class="px-2 py-2" style="border-radius: 0%">
          <v-card-text class="pb-0"> IP ADDRESS </v-card-text>

          <v-card-title class="d-flex">
            {{ props.ipInfo.address }}
          </v-card-title>
        </v-card>
      </v-col>

      <v-col cols="3" class="pa-0">
        <v-card elevation="0" class="px-2 py-2" style="border-radius: 0%">
          <v-card-text class="pb-0"> LOCATION </v-card-text>

          <v-card-title class="">
            {{ props.ipInfo.state }}
          </v-card-title>
        </v-card>
      </v-col>

      <v-col cols="3" class="pa-0">
        <v-card elevation="0" class="px-2 py-2" style="border-radius: 0%">
          <v-card-text class="pb-0"> TIMEZONE </v-card-text>

          <v-card-title class="">
            {{ props.ipInfo.timezone }}
          </v-card-title>
        </v-card>
      </v-col>

      <v-col cols="3" class="pa-0">
        <v-card elevation="0" class="px-2 py-2" style="border-radius: 0%">
          <v-card-text class="pb-0"> ISP </v-card-text>

          <v-card-title style="flex-wrap: wrap" class="d-flex flex-column">
            {{ props.ipInfo.isp }}
          </v-card-title>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, defineProps } from "vue";

// const info = ref(["IP ADDRESS", "LOCATION", "TIMEZONE", "ISP"]);

// const title = ref([
//   "192.212.174.101",
//   "Elkelaa des sraghna",
//   "UTC-05:00",
//   "Clever schule",
// ]);

const props = defineProps({
  ipInfo: {
    type: Object,
  },
});
</script>
