<script setup lang="ts">
import { Button } from '@/components/ui/button';
import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from '@/components/ui/table';
import { SearchInput } from "@/components/ui/search";
import AppLayout from '@/layouts/AppLayout.vue';
import type { BreadcrumbItem } from '@/types';
import { Head, Link } from '@inertiajs/vue3';
import { defineProps } from 'vue';

const breadcrumbs: BreadcrumbItem[] = [
    {
        title: 'Dashboard',
        href: '/admin/dashboard',
    },
    {
        title: 'Items',
        href: '/admin/items',
    },
];

defineProps<{
    items: Array;
}>();
</script>

<template>
    <Head title="Dashboard" />

    <AppLayout :breadcrumbs="breadcrumbs">
        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="flex justify-between items-center">
                    <h3 class="text-2xl">Items</h3>
                    <SearchInput route-name="admin.items.index" />
                </div>
                <div class="flex justify-end py-4">
                    <Button :as="Link" :href="route('admin.items.create')">Create Item</Button>
                </div>

                <div class="mt-8 flex flex-col">
                    <Table>
                        <TableHeader>
                            <TableRow>
                                <TableHead>Name</TableHead>
                                <TableHead>Type</TableHead>
                                <TableHead>Description</TableHead>
                                <TableHead>Active</TableHead>
                                <TableHead>Actions</TableHead>
                            </TableRow>
                        </TableHeader>
                        <TableBody>
                            <TableRow v-for="item in items" :key="item.id">
                                <TableCell>
                                    {{ item.name }}
                                </TableCell>
                                <TableCell>{{ item.content_type }}</TableCell>
                                <TableCell>{{ item.description }}</TableCell>
                                <TableCell>{{ item.active ? 'Active' : 'Inactive' }}</TableCell>
                                <TableCell class="w-40 px-0">
                                    <Button :as="Link" variant="link" :href="route('admin.items.edit', item.id)"> Edit </Button>
                                    <Button :as="Link" variant="link" :href="route('admin.items.delete', item.id)"> Delete </Button>
                                </TableCell>
                            </TableRow>
                        </TableBody>
                    </Table>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
