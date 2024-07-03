<script setup lang="ts">
import Toast from 'primevue/toast';
import AppHeader from './partials/AppHeader.vue';
import AppSidebar from './partials/AppSidebar.vue';
import { ref } from 'vue';

const sideBarOpen = ref(false);
</script>

<template>
    <div class="flex h-screen overflow-hidden">
        <AppSidebar :is-sidebar-open="sideBarOpen" @updatesidebar="(value: boolean) => (sideBarOpen = value)" />
        <div class="relative flex flex-1 flex-col overflow-y-auto overflow-x-hidden">
            <AppHeader :is-sidebar-open="sideBarOpen" @updatesidebar="(value: boolean) => (sideBarOpen = value)" />
            <main class="h-full">
                <Toast />
                <slot />
            </main>
        </div>
    </div>
</template>
