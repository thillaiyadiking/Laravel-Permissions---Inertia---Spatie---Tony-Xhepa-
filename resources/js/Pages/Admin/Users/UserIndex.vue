<script setup>
import AdminLayout from '@/Layouts/AdminLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';
import Table from '@/Components/Table.vue';
import TableRow from '@/Components/TableRow.vue';
import TableHeaderCell from '@/Components/TableHeaderCell.vue';
import TableDataCell from '@/Components/TableDataCell.vue';
import { ref } from 'vue';
import Modal from '@/Components/Modal.vue';
import DangerButton from '@/Components/DangerButton.vue';
import SecondaryButton from '@/Components/SecondaryButton.vue';

defineProps(['users'])

const form = useForm({});

const showConfirmDeleteUserModal = ref(false);
const confirmDeleteUser = () => {
    showConfirmDeleteUserModal.value = true
}
const closeModal = () => {
    showConfirmDeleteUserModal.value = false
}
const deleteUser = (id) => {
    form.delete(route('users.destroy', id), {
        onSuccess: () => closeModal()
    })
}
</script>

<template>

    <Head title="Users" />

    <!-- <AdminLayout> -->
    <!-- <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Dashboard</h2>
        </template> -->


    <div>
        <div class="flex justify-between">
            <h1>Welcome User Index Page</h1>
            <Link :href="route('users.create')"
                class="middle none center mr-3 rounded-lg bg-pink-900 py-3 px-6 font-sans text-xs font-bold uppercase text-white shadow-md shadow-pink-500/20 transition-all hover:shadow-lg hover:shadow-pink-500/40 focus:opacity-[0.85] focus:shadow-none active:opacity-[0.85] active:shadow-none disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none">
            New User
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
                                <TableHeaderCell>Email</TableHeaderCell>
                                <TableHeaderCell>Action</TableHeaderCell>
                            </TableRow>
                        </template>
                        <template #default>
                            <TableRow v-for="(user, index) in users" :key="user.id">
                                <TableDataCell>{{ user.id }}</TableDataCell>
                                <TableDataCell>{{ user.name }}</TableDataCell>
                                <TableDataCell>{{ user.email }}</TableDataCell>
                                <TableDataCell class="text-indigo-600 hover:text-indigo-900 space-x-4">
                                    <Link :href="route('users.edit', user.id)"
                                        class="text-green-400 hover:text-green-600">
                                    Edit
                                    </Link>
                                    <!-- <Link :href="route('users.destroy', user.id)" method="DELETE" as="button"
                                        class="text-red-400 hover:text-red-600">
                                    Delete
                                    </Link> -->
                                    <button class="text-red-400 hover:text-red-600"
                                        @click="confirmDeleteUser">Delete</button>
                                    <Modal :show="showConfirmDeleteUserModal" @close="closeModal">
                                        <div class="p-6">
                                            <h2 class="text-lg font-semibold text-white">
                                                Are you sure you want to delete this user?
                                            </h2>
                                            <div class="mt-6 flex space-x-4">
                                                <DangerButton @click="deleteUser(user.id)">
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
