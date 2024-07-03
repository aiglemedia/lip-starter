<script setup lang="ts">
import {Head} from '@inertiajs/vue3';
import PageHeader from "@/Pages/PageHeader.vue";
import ApplicationLogo from "@/Components/ApplicationLogo.vue";

</script>

<template>
    <Head title="Dashboard" />
    <PageHeader title="Dashboard"/>
    <div class="p-2 lg:p-4">
        <div class="flex flex-col h-screen justify-around items-center p-4">
        <div class="flex flex-col justify-center items-center">
            <ApplicationLogo alt="Logo" class="mb-8 h-40" />
            <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold text-center text-gray-700 mb-4">
                Laravel Inertiajs Primevue.
            </h1>
            <p class="text-center text-gray-500 text-lg md:text-xl lg:text-2xl mb-8">
                A starter template based on Laravel Inertiajs and Primevue!
            </p>
        </div>
        <div class="flex justify-center">
            <div class="text-sm text-gray-500">
                Copyrights - {{ new Date().getFullYear() }}
            </div>
        </div>
    </div>
    </div>
</template>
