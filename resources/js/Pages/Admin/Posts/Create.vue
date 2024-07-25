<script setup>
import AdminLayout from '@/Layouts/AdminLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import VueMultiselect from 'vue-multiselect'


// defineProps({
//     permissions: Array
// })
const form = useForm({
    'title': '',
    // permissions: []
})
</script>

<template>

    <Head title="Create New Post" />

    <!-- <AdminLayout> -->
    <!-- <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Dashboard</h2>
        </template> -->


    <div class="max-w-md mx-auto bg-slate-100 shadow-lg rounded-lg p-6">
        <div class="flex justify-between">
            <h1>Create Post Page</h1>
            <Link :href="route('posts.index')"
                class="middle none center mr-3 rounded-lg bg-pink-900 py-3 px-6 font-sans text-xs font-bold uppercase text-white shadow-md shadow-pink-500/20 transition-all hover:shadow-lg hover:shadow-pink-500/40 focus:opacity-[0.85] focus:shadow-none active:opacity-[0.85] active:shadow-none disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none">
            Back
            </Link>
        </div>
        <div class="flex flex-col mt-2">
            <div class="py-2 -my-2 overflow-x-auto sm:-mx-6 sm:px-6 lg:-mx-8 lg:px-8">
                <form @submit.prevent="form.post(route('posts.store'))">
                    <div class="mt-4">
                        <InputLabel for="title" value="Title" />

                        <TextInput id="title" type="text" class="mt-1 block w-full" v-model="form.title" />

                        <InputError class="mt-2" :message="form.errors.title" />
                    </div>




                    <div class="flex items-center mt-4">

                        <PrimaryButton class="ms-4 bg-pink-400" :class="{ 'opacity-25': form.processing }"
                            :disabled="form.processing">
                            Create
                        </PrimaryButton>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- </AdminLayout> -->
</template>
<script>
export default {
    layout: AdminLayout
}
</script>
