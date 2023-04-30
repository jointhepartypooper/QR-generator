<template>
  <qrcode-vue v-if="message.length>2"
    :value="message"
    :size="700"
    render-as="svg"
    :margin="3"
    level="H"
  />
  <h5 id="header1">QR message</h5>
  <textarea  id="styled" v-model="message" placeholder="..."> </textarea>
</template>

<script lang="ts" setup>
import { ref, onMounted } from "vue";
import QrcodeVue from "qrcode.vue";

onMounted(() => {
  let result = "" as string | null;
  let queryString = window.location.search;
  let urlParams = new URLSearchParams(queryString);

  if (urlParams.has("qr")) {
    result = urlParams.get("qr");
  }

  message.value = !!result ? decodeURI(result) : "";
});
 
const message = ref<string>("");
 
</script>

<style scoped>
#header1{
    color:rgb(17, 17, 56);
}
textarea#styled {
  width: 600px;
  height: 120px;
  border: 3px solid #cccccc;
  padding: 5px;
  font-family: Tahoma, sans-serif;
  background-position: bottom right;
  background-repeat: no-repeat;
}
</style>
