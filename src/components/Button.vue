<template>
  <button
    @click="$emit('btnClick')"
    :style="{ background: bgColor, color: textColor }"
    class="btn"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    bgColor: String,
    textColor: String,
  },
}
</script>

<style></style>
