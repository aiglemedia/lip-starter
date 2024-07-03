<script setup lang="ts">
import GuestLayout from '@/Layouts/GuestLayout.vue';
import Checkbox from 'primevue/checkbox';
import { Head, Link, useForm } from '@inertiajs/vue3';
import InputText from 'primevue/inputtext';
import FormError from '@/Components/FormError.vue';
import Button from 'primevue/button';

defineOptions({
    layout: GuestLayout,
});

defineProps<{
    canResetPassword?: boolean;
    status?: string;
}>();

const form = useForm({
    email: 'test@example.com',
    password: 'password',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => {
            form.reset('password');
        },
    });
};
</script>
<style>
.labelclass {
    @apply block font-medium text-sm max-w-max;
}
</style>
<template>

    <Head title="Log in" />

    <div class="max-w-md sm:w-full mx-auto mt-6 px-6 py-4 bg-white shadow-md overflow-hidden sm:rounded-lg">
        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>

        <form @submit.prevent="submit" class="mt-1 space-y-4">
            <div class="flex flex-col gap-1">
                <label class="labelclass" for="email">Email</label>
                <InputText id="email" type="email" autofocus v-model="form.email"
                    :class="form.errors.email ? '!border-red-300' : ''" />
                <FormError :message="form.errors.email" />
            </div>
            <div class="flex flex-col gap-1">
                <label class="labelclass" for="password">Password</label>
                <InputText id="password" type="password" v-model="form.password"
                    :class="form.errors.password ? '!border-red-300' : ''" />
                <FormError :message="form.errors.password" />
            </div>
            <div class="block">
                <Checkbox v-model="form.remember" inputId="remember" name="remember" />
                <label for="remember" class="ml-2">Remember me</label>
            </div>
            <div class="flex items-center justify-end gap-2">
                <Link v-if="canResetPassword" :href="route('password.request')"
                    class="underline text-sm text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                Forgot your password?
                </Link>
                <Button :class="{ 'opacity-25': form.processing }" :disabled="form.processing" label="Log in"
                    size="small" type="submit" />
            </div>
        </form>
    </div>
</template>
