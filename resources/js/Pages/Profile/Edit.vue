<script setup lang="ts">
import DeleteUserForm from './Partials/DeleteUserForm.vue';
import UpdatePasswordForm from './Partials/UpdatePasswordForm.vue';
import UpdateProfileInformationForm from './Partials/UpdateProfileInformationForm.vue';
import { Head } from '@inertiajs/vue3';
import PageHeader from "@/Pages/PageHeader.vue";

defineProps<{
    mustVerifyEmail?: boolean;
    status?: string;
}>();
</script>

<template>
    <Head title="Profile" />
    <PageHeader title="Profile / Edit" />
    <div class="p-3 lg:p-4 mt-1 bg-white">
        <div class="p-4 bg-gray-50 shadow sm:rounded-lg space-y-4">
            <div class="p-4 sm:p-8 bg-white shadow sm:rounded-lg">
                <UpdateProfileInformationForm
                    :must-verify-email="mustVerifyEmail"
                    :status="status"
                    class="max-w-xl"
                />
            </div>

            <div class="p-4 sm:p-8 bg-white shadow sm:rounded-lg">
                <UpdatePasswordForm class="max-w-xl" />
            </div>

<!--            <div class="p-4 sm:p-8 bg-white shadow sm:rounded-lg">-->
<!--                <DeleteUserForm class="max-w-xl" />-->
<!--            </div>-->
        </div>
    </div>
</template>
