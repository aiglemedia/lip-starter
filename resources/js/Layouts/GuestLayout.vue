<script setup lang="ts">
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import { Link } from '@inertiajs/vue3';
import Toast from "primevue/toast";

</script>

<template>
    <div class="min-h-screen bg-gray-100">
        <Toast />
        <header class="sticky top-0 z-999 flex w-full bg-gray-50 shadow-md">
            <div class="flex flex-grow items-center justify-between py-4 px-4">
                <div class="flex items-center gap-2">
                    <Link :href="route('home')">
                        <ApplicationLogo class="w-6 h-6" />
                    </Link>
                </div>
                <div class="grow"></div>
                <div class="flex items-center">
                    Version 1.0
                </div>
            </div>
        </header>
        <main>
            <slot />
        </main>
    </div>
</template>
