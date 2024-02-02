<template>
  <main class="container">
    <div class="d-flex flex-column" style="position: relative">
      <img height="230" src="../assets/pattern-bg-desktop.png" />
      <div
        class="d-flex flex-column align-center"
        style="
          z-index: 9999;
          position: absolute;
          left: 50%;
          top: 2%;
          transform: translateX(-50%);
        "
      >
        <h1>IP Address Tracker</h1>

        <v-text-field
          v-model="queryIp"
          class="py-6"
          variant="solo"
          style="width: 550px; position: relative"
          label="Search for any IP address or leave empty to get your ip info"
          ><v-btn
            @click="getIpInfo"
            elevation="0"
            class="py-7 align-center d-flex"
            style="
              z-index: 1;
              background: black;
              position: absolute;
              right: 0;
              top: 0;
              border-top-left-radius: 0%;
              border-bottom-left-radius: 0%;
            "
            ><img src="../assets/icon-arrow.svg" alt="" /></v-btn
        ></v-text-field>

        <!-- //Ip info -->
        <IpInfo v-if="ipInfo" :ipInfo="ipInfo" style="z-index: 500" />
      </div>
      <!-- Map -->
      <div ref="mapContainer" style="height: 70vh; width: 1520px"></div>
    </div>
  </main>
</template>

<script setup>
import IpInfo from "../components/IpInfo.vue";
import { ref, onMounted } from "vue";
import L from "leaflet";
import axios from "axios";

const map = ref();
const mapContainer = ref();

onMounted(() => {
  map.value = L.map(mapContainer.value).setView([51.505, -0.09], 13);

  L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
    maxZoom: 18,
    attribution:
      '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
  }).addTo(map.value);
});

const queryIp = ref("");
const ipInfo = ref(null);
const drag = ref();

const getIpInfo = async () => {
  try {
    const data = await axios.get(`http://ipwho.is/${queryIp.value}`);

    const result = data.data;

    ipInfo.value = {
      address: result.ip,
      state: result.region,
      timezone: result.timezone.utc,
      isp: result.connection.isp,
      lat: result.latitude,
      lng: result.longitude,
    };

    console.log(result);

    L.marker([ipInfo.value.lat, ipInfo.value.lng], { draggable: true }).addTo(
      map.value
    );
    // .on("dragend", (event) => {
    //   drag.value = event;
    //   console.log(drag);
    // });

    map.value.setView([ipInfo.value.lat, ipInfo.value.lng], 13);
  } catch (err) {
    alert(err.message);
  }
};
</script>
