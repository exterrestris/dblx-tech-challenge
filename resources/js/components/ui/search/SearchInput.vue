<script setup lang="ts">
import { ref, watch } from 'vue';
import { router } from '@inertiajs/vue3'
import { XIcon } from 'lucide-vue-next';
import { debounce } from 'lodash';
import { Button } from '@/components/ui/button';

const props = defineProps({
    routeName: {
        type: String,
        required: true,
    },
});

let search = ref(null);
let sort = ref(null);
let searchRef = ref(null);

watch(search, () => {
    if (search.value) {
        searchMethod();
    } else {
        router.get(route(props.routeName));
    }
});

const searchMethod = debounce(() => {
    router.get(
        route(props.routeName),
        { search: search.value, sort: sort.value },
        { preserveState: true }
    );
}, 2000);
</script>

<template>
    <div class="w-1/4 bg-white dark:bg-gray-800 relative">
        <label for="search" class="hidden">Search</label>
        <input
            id="search"
            ref="searchRef"
            v-model="search"
            class="h-10 w-full cursor-pointer rounded-full border border-gray-500 bg-gray-100 pl-4 pr-8 pb-0 pt-px text-gray-700 outline-none"
            autocomplete="off"
            name="search"
            placeholder="Search"
            type="search"
            value={search.value}
            @keyup.esc="search = null"
        />
        <button
            class="absolute right-2 top-0 translate-y-1/2 px-1"
            @click="search = null"
        >
            <component :is="XIcon" class="h-5 w-5 text-gray-700" />
            <span class="hidden">Clear</span>
        </button>
    </div>
</template>
