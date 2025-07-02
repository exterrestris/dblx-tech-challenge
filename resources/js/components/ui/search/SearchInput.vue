<script setup lang="ts">
import { ref, watch } from 'vue';
import { router } from '@inertiajs/vue3'
import { debounce } from 'lodash';

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
    <div class="w-1/4 bg-white dark:bg-gray-800">
        <label for="search" class="hidden">Search</label>
        <input
            id="search"
            ref="searchRef"
            v-model="search"
            class="h-10 w-full cursor-pointer rounded-full border border-gray-500 bg-gray-100 px-4 pb-0 pt-px text-gray-700 outline-none"
            autocomplete="off"
            name="search"
            placeholder="Search"
            type="search"
            value={search.value}
            @keyup.esc="search = null"
        />
    </div>
</template>
