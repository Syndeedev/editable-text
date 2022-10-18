<template>
  <div class="app">
    <div class="">Vue 3 with typescript {{ age }}</div>
    <editable-content
      :text="state.text"
      :fields="state.fields"
      @emitValues="getValues($event)"
    />
    <router-view />
  </div>
</template>
<script lang="ts" setup>
import { reactive, ref } from "vue";
import EditableContent from "./components/EditableContent.vue";

const age = ref<number | string>(25);
const state = reactive({
  text: "The best {industry} Platform for Multi-Location Brands. Kindly visit our website: {url} or call us on {phone}. Great doing {busness with you!",
  fields: {
    industry: {
      default: "Marketing",
      type: "text",
    },
    url: {
      default: "https://googlemybusiness.com/app",
      type: "url",
    },
    phone: {
      default: "+2348175020329",
      type: "text",
    },
  },
});

const getValues = (values: any) => {
  console.log({ values }, "omooo");
};
</script>

<style></style>
