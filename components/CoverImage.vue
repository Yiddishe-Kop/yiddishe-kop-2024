<script setup lang="ts">
import { computed } from "vue";

const props = defineProps<{
  src: string;
  alt: string;
}>();

const imageSrc = computed(() => {
  return props.src[0] == "/"
    ? props.src
    : `https://source.unsplash.com/${props.src}`;
});
</script>

<template>
  <NuxtImg :src="imageSrc" />
</template>
