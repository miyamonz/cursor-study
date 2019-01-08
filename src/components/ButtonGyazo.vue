<template>
  <button @click="click">gyazo</button>
</template>
<script>
import axios from "axios";
export default {
  methods: {
    click() {
      const canvas = document.querySelector("canvas.drawer");
      if (!canvas) return;

      const dataURL = canvas.toDataURL();
      this.send(dataURL);
    },
    async send(image_url) {
      const url = "https://upload.gyazo.com/api/upload/easy_auth";
      const params = new URLSearchParams();
      params.append(
        "client_id",
        "e2c8616d74bcb1c1eb4b879f74506987e9bc6b5c7be99b437295ccf26ef44a12"
      );
      params.append("image_url", image_url);
      params.append("referer_url", window.location.href);
      const res = await axios.post(url, params);
      const { get_image_url } = res.data;
      window.open(get_image_url);
    }
  }
};
</script>
