<script setup lang="ts">
import { BookOpen, Download, ExternalLink } from 'lucide-vue-next';

defineProps<{
    item: object
}>()

const iconMap = {
    "book-open": BookOpen,
    "download": Download,
    "external-link": ExternalLink,
}
</script>

<template>
    <div class="relative w-full">
        <div class="flex absolute top-0 left-0 w-full">
            <div class="bg-black p-4 float-left left-0 top-0">
                <component :is="iconMap[item.type_icon]" class="h-5 w-5 text-white"/>
            </div>
            <p class="bg-black text-white p-4 flex-grow">{{ item.name }}</p>
        </div>
        <img class="object-cover" :src="item.image_url" :alt="item.name" />
    </div>
</template>
