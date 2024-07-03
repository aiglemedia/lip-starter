<template>
  <header class="bg-white shadow">
    <div class="py-6 px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between">
        <h2 class="font-semibold text-xl text-gray-800 leading-tight">{{ props.title }}</h2>
      </div>
    </div>
  </header>
</template>
<script lang="ts" setup>
type HeaderProp = {
    title: string;
};
const props = defineProps<HeaderProp>();
</script>
