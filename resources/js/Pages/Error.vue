<script setup lang="ts">
import { computed } from 'vue';
import Button from "primevue/button";

defineOptions({ layout: '' })
const props = defineProps<{
    status: number
}>()

const title = computed(() => {
    return {
        503: '503: Service Unavailable',
        500: '500: Server Error',
        404: '404: Page Not Found',
        403: '403: Forbidden',
    }[props.status]
})

const description = computed(() => {
    return {
        503: 'Sorry, we are doing some maintenance. Please check back soon.',
        500: 'Whoops, something went wrong on our servers.',
        404: 'Sorry, the page you are looking for could not be found.',
        403: 'Sorry, you are forbidden from accessing this page.',
    }[props.status]
})
const goback = () => {
    window.history.back();
}
</script>

<template>
    <div class="flex flex-col h-screen justify-center items-center p-2 bg-white">
        <div class="max-w-max p-4 bg-gray-100">
            <h1>{{ title }}</h1>
            <div>{{ description }}</div>
            <Button label="Back" severity="secondary" size="small" @click="goback()" />
        </div>
    </div>
</template>
