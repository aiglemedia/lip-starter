<script setup lang="ts">
import GuestLayout from '@/Layouts/GuestLayout.vue';
import { Head, useForm } from '@inertiajs/vue3';
import InputText from "primevue/inputtext";
import FormError from "@/Components/FormError.vue";
import Button from "primevue/button";

defineOptions({
    layout: GuestLayout
})

defineProps<{
    status?: string;
}>();

const form = useForm({
    email: '',
});

const submit = () => {
    form.post(route('password.email'));
};
</script>
<style>
.labelclass {
    @apply block font-medium text-sm max-w-max
}
</style>
<template>
    <Head title="Forgot Password" />
    <div class="flex flex-col justify-center items-center w-full">
        <div class="p-4 max-w-md">
            <div class="mb-4 text-sm text-gray-600">
            Forgot your password? No problem. Just let us know your email address and we will email you a password reset
            link that will allow you to choose a new one.
        </div>
        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>

        <form @submit.prevent="submit" class="mt-1 space-y-4">
            <div class="flex flex-col gap-1">
                <label class="labelclass" for="email">Email</label>
                <InputText id="email" type="email" autofocus v-model="form.email" :class="form.errors.email ? '!border-red-300' : ''" />
                <FormError :message="form.errors.email" />
            </div>
            <div class="flex items-center justify-end">
                <Button class="w-full" :class="{ 'opacity-25': form.processing }" :disabled="form.processing" label="Email Password Reset Link"
                        size="small" type="submit"/>
            </div>
        </form>
        </div>
    </div>
</template>
