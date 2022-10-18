<template>
  <div>
    <div @input="onInput($event)" v-html="displayText()"></div>
  </div>
</template>

<script lang="ts" setup>
import { computed, defineProps, defineEmits, toRaw } from "vue";
const props = defineProps({
  text: {
    type: String,
    required: true,
  },
  fields: {
    type: Object,
    required: true,
  },
});
const fields = toRaw(props.fields);
const values: any = computed(() => {
  if (!fields) return;
  const result = Object.assign(
    {},
    ...Object.entries(fields).map(([key, value]) => ({ [key]: value.default }))
  );

  return result;
});
const emit = defineEmits(["emitValues"]);
const displayText = () => {
  const newTextArray = props.text.split(" ");
  const processedArray: any = [];
  newTextArray.forEach((element) => {
    element = element.replace(/\.$/, "");
    const singleelement: any = element.slice(1, -1);
    if (element.includes("{") && values.value[singleelement]) {
      element = `<span style="cursor: pointer;" class='${singleelement}' contenteditable >${values.value[singleelement]}</span>`;
    }
    processedArray.push(element);
  });
  return processedArray.join(" ");
};
const onInput = (e: any) => {
  values.value[e.target.className] = e.target.innerText;
  emit("emitValues", values.value);
};
</script>

<style lang="scss" scoped></style>
