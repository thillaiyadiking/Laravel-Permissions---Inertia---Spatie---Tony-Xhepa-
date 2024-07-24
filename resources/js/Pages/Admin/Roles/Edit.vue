<script setup>
import AdminLayout from '@/Layouts/AdminLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';



import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import VueMultiselect from 'vue-multiselect'

import Table from '@/Components/Table.vue';
import TableRow from '@/Components/TableRow.vue';
import TableHeaderCell from '@/Components/TableHeaderCell.vue';
import TableDataCell from '@/Components/TableDataCell.vue';
import { onMounted, watch } from 'vue';

const props = defineProps({
    role: {
        type: Object,
        required: true
    },
    permissions: Array
})

const form = useForm({
    'name': props.role.name,
    permissions: []
})

onMounted(() => {
    form.permissions = props.role?.permissions
})

watch(() => props.role, () => (form.permissions = props.role?.permissions))
</script>

<template>

    <Head title="Update Role" />

    <!-- <AdminLayout> -->
    <!-- <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Dashboard</h2>
        </template> -->


    <div class="max-w-7xl mx-auto py-4">
        <div class="flex justify-between">
            <h1>Update Role Page</h1>
            <Link :href="route('roles.index')"
                class="middle none center mr-3 rounded-lg bg-pink-900 py-3 px-6 font-sans text-xs font-bold uppercase text-white shadow-md shadow-pink-500/20 transition-all hover:shadow-lg hover:shadow-pink-500/40 focus:opacity-[0.85] focus:shadow-none active:opacity-[0.85] active:shadow-none disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none">
            Back
            </Link>
        </div>

        <div class="max-w-md mx-auto bg-slate-100 shadow-lg rounded-lg p-6">
            <h1 class="text-2xl font-semibold text-indigo-700">Update Role</h1>
            <form @submit.prevent="form.put(route('roles.update', role.id))">
                <div class="mt-4">
                    <InputLabel for="name" value="Name" />

                    <TextInput id="name" type="text" class="mt-1 block w-full" v-model="form.name" />

                    <InputError class="mt-2" :message="form.errors.name" />
                </div>

                <div class="mt-4">
                    <InputLabel for="permissions" value="Permissions" />
                    <VueMultiselect v-model="form.permissions" :options="permissions" :multiple="true"
                        :close-on-select="true" placeholder="Pick some" label="name" track-by="name" />
                </div>

                <div class="flex items-center mt-4">

                    <PrimaryButton class="ms-4 bg-pink-400" :class="{ 'opacity-25': form.processing }"
                        :disabled="form.processing">
                        Update
                    </PrimaryButton>
                </div>
            </form>
        </div>
        <div class="mt-6 max-w-md mx-auto bg-slate-100 shadow-lg rounded-lg p-6">
            <h1 class="text-2xl font-semibold text-indigo-700">Permissions</h1>
            <div class="bg-white">
                <Table>
                    <template #header>
                        <TableRow>
                            <TableHeaderCell>ID</TableHeaderCell>
                            <TableHeaderCell>Name</TableHeaderCell>
                            <!-- <TableHeaderCell>Email</TableHeaderCell> -->
                            <TableHeaderCell>Action</TableHeaderCell>
                        </TableRow>
                    </template>
                    <template #default>
                        <TableRow v-for="(rolePermission, index) in role.permissions" :key="rolePermission.id">
                            <TableDataCell>{{ rolePermission.id }}</TableDataCell>
                            <TableDataCell>{{ rolePermission.name }}</TableDataCell>
                            <!-- <TableDataCell>{{ rolePermission.email }}</TableDataCell> -->
                            <TableDataCell class="text-indigo-600 hover:text-indigo-900 space-x-4">

                                <Link :href="route('roles.permissions.destroy', [role.id, rolePermission.id])"
                                    method="DELETE" as="button" class="text-red-400 hover:text-red-600">
                                Revoke
                                </Link>
                            </TableDataCell>
                        </TableRow>
                    </template>
                </Table>
            </div>
        </div>

    </div>

    <!-- </AdminLayout> -->
</template>
<style src="vue-multiselect/dist/vue-multiselect.css"></style>

<script>
export default {
    layout: AdminLayout
}
</script>
