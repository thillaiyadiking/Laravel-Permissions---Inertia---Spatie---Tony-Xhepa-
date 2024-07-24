<script setup>
import AdminLayout from '@/Layouts/AdminLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';
import Table from '@/Components/Table.vue';
import TableRow from '@/Components/TableRow.vue';
import TableHeaderCell from '@/Components/TableHeaderCell.vue';
import TableDataCell from '@/Components/TableDataCell.vue';


import Checkbox from '@/Components/Checkbox.vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';

const props = defineProps({
    permission: {
        type: Object,
        required: true
    }
})

const form = useForm({
    'name': props.permission?.name
})
</script>

<template>

    <Head title="Update Permission" />

    <!-- <AdminLayout> -->
    <!-- <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Dashboard</h2>
        </template> -->


    <div class="max-w-md mx-auto bg-slate-100 shadow-lg rounded-lg p-6">
        <div class="flex justify-between">
            <h1>Update Permission Page</h1>
            <Link :href="route('permission.index')"
                class="middle none center mr-3 rounded-lg bg-pink-900 py-3 px-6 font-sans text-xs font-bold uppercase text-white shadow-md shadow-pink-500/20 transition-all hover:shadow-lg hover:shadow-pink-500/40 focus:opacity-[0.85] focus:shadow-none active:opacity-[0.85] active:shadow-none disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none">
            Back
            </Link>
        </div>
        <div class="flex flex-col mt-8">
            <div class="py-2 -my-2 overflow-x-auto sm:-mx-6 sm:px-6 lg:-mx-8 lg:px-8">
                <form @submit.prevent="form.put(route('permission.update', permission.id))">
                    <div>
                        <InputLabel for="name" value="Name" />

                        <TextInput id="name" type="text" class="mt-1 block w-full" v-model="form.name" />

                        <InputError class="mt-2" :message="form.errors.name" />
                    </div>



                    <div class="flex items-center mt-4">

                        <PrimaryButton class="ms-4 bg-pink-400" :class="{ 'opacity-25': form.processing }"
                            :disabled="form.processing">
                            Updtate
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
