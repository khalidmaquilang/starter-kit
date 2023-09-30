<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <div class="w-full mx-auto">
            <div class="p-6 text-base-content">You're logged in!</div>
        </div>
    </AuthenticatedLayout>
</template>
