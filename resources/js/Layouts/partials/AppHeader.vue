<script setup lang="ts">
import { Link } from '@inertiajs/vue3';
import Button from 'primevue/button';
import DropdownUser from './DropdownUser.vue'
import ApplicationLogo from "@/Components/ApplicationLogo.vue";

type SidebarProp = {
    isSidebarOpen: boolean;
};
const props = defineProps<SidebarProp>();
const emit = defineEmits<{
    updatesidebar: [value: boolean]
}>()
</script>

<template>
  <header class="sticky top-0 z-999 flex w-full bg-gray-50 shadow-md">
    <div class="flex flex-grow items-center justify-between py-4 px-4">
      <div class="flex items-center gap-2 lg:hidden">
          <Button text icon="pi pi-bars" @click="emit('updatesidebar', !props.isSidebarOpen)" />
          <Link :href="route('home')">
              <ApplicationLogo class="text-xl" />
          </Link>
      </div>
      <div class="grow"></div>
      <div class="flex items-center">
        <DropdownUser />
      </div>
    </div>
  </header>
</template>
