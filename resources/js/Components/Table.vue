<script setup>
</script>
<template>
    <div>
        <table class="min-w-full">
            <thead>
                <slot name="header"></slot>
            </thead>

            <tbody class="bg-white">
                <slot />
            </tbody>
        </table>
    </div>
</template>