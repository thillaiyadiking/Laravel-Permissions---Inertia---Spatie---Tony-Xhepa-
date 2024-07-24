<script setup>
import AdminLayout from '@/Layouts/AdminLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

import Table from '@/Components/Table.vue';
import TableRow from '@/Components/TableRow.vue';
import TableHeaderCell from '@/Components/TableHeaderCell.vue';
import TableDataCell from '@/Components/TableDataCell.vue';

import Modal from '@/Components/Modal.vue';
import DangerButton from '@/Components/DangerButton.vue';
import SecondaryButton from '@/Components/SecondaryButton.vue';
import { ref } from 'vue';
defineProps(['permissions'])



const form = useForm({});

const showConfirmDeletePermissionModal = ref(false);
const confirmDeletePermission = () => {
    showConfirmDeletePermissionModal.value = true
}
const closeModal = () => {
    showConfirmDeletePermissionModal.value = false
}
const deletePermission = (id) => {
    form.delete(route('permission.destroy', id), {
        onSuccess: () => closeModal()
    })
}
</script>

<template>

    <Head title="Permission" />

    <!-- <AdminLayout> -->
    <!-- <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Dashboard</h2>
        </template> -->


    <div>
        <div class="flex justify-between">
            <h1>Welcome Permission Index Page</h1>
            <Link :href="route('permission.create')"
                class="middle none center mr-3 rounded-lg bg-pink-900 py-3 px-6 font-sans text-xs font-bold uppercase text-white shadow-md shadow-pink-500/20 transition-all hover:shadow-lg hover:shadow-pink-500/40 focus:opacity-[0.85] focus:shadow-none active:opacity-[0.85] active:shadow-none disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none">
            New Permission
            </Link>
        </div>
        <div class="flex flex-col mt-8">
            <div class="py-2 -my-2 overflow-x-auto sm:-mx-6 sm:px-6 lg:-mx-8 lg:px-8">
                <div
                    class="inline-block min-w-full overflow-hidden align-middle border-b border-gray-200 shadow sm:rounded-lg">
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
                            <TableRow v-for="(permission, index) in permissions" :key="permission.id">
                                <TableDataCell>{{ permission.id }}</TableDataCell>
                                <TableDataCell>{{ permission.name }}</TableDataCell>
                                <!-- <TableDataCell>{{ permission.email }}</TableDataCell> -->
                                <TableDataCell class="text-indigo-600 hover:text-indigo-900 space-x-4">
                                    <!-- Edit / Delete -->
                                    <Link :href="route('permission.edit', permission.id)"
                                        class="text-green-400 hover:text-green-600">
                                    Edit
                                    </Link>
                                    <!-- <Link :href="route('permission.destroy', permission.id)" method="DELETE" as="button"
                                        class="text-red-400 hover:text-red-600">
                                    Delete
                                    </Link> -->
                                    <button class="text-red-400 hover:text-red-600"
                                        @click="confirmDeletePermission">Delete</button>
                                    <Modal :show="showConfirmDeletePermissionModal" @close="closeModal">
                                        <div class="p-6">
                                            <h2 class="text-lg font-semibold text-white">
                                                Are you sure you want to delete this permission?
                                            </h2>
                                            <div class="mt-6 flex space-x-4">
                                                <DangerButton @click="deletePermission(permission.id)">
                                                    Delete
                                                </DangerButton>
                                                <SecondaryButton @click="closeModal">
                                                    Cancel
                                                </SecondaryButton>
                                            </div>
                                        </div>
                                    </Modal>
                                </TableDataCell>
                            </TableRow>
                        </template>
                    </Table>
                </div>
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
