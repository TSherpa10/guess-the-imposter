<template>
    <div v-if="isLoading">
        <LoadingPage/>
    </div>
    <div v-else class="flex items-center justify-center h-screen w-full">
        <h1 class="text-6xl">landing page</h1>
        <Button label='Start Loading' @click="startLoading"/>
    </div>
</template>

<script setup lang="ts">
import Button from 'primevue/button';
import { ref } from 'vue';
import LoadingPage from './LoadingPage.vue';

const isLoading = ref(false);

function startLoading() {
    isLoading.value = !isLoading.value;
}
</script>