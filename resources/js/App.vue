<template>
    <router-view v-slot="{ Component, route }">
        <div :key="route.name">
            <Component :is="Component" />
        </div>
    </router-view>
</template>
<script setup>
import axios from "axios";
import { ref } from "vue";

const response = ref();

const getValue = async () => {
    try {
        response.value = await axios.get("/api/test-me");
    } catch (error) {
        // Do something with the error
        console.log(error);
    }
};

</script>