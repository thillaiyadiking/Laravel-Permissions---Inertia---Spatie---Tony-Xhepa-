<script setup>
import { computed } from 'vue';
import { Link } from '@inertiajs/vue3';

const props = defineProps({
    href: {
        type: String,
        required: true,
    },
    active: {
        type: Boolean,
    },
});

const classes = computed(() =>
    props.active
        ? 'flex items-center px-6 py-2 mt-4 text-gray-100 bg-gray-700 bg-opacity-25'
        : 'flex items-center px-6 py-2 mt-4 text-gray-500 hover:bg-gray-700 hover:bg-opacity-25 hover:text-gray-100'
);
</script>

<template>
    <Link :href="href" :class="classes">
    <slot />
    </Link>
</template>
