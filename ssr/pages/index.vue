<script setup lang="ts">
import dayjs from "dayjs"

useHead({
    title: 'Nuxt3 SSR Example',
})

const count = ref(0)

const clientDate = ref()
onMounted(() => {
    clientDate.value = dayjs().toString()
})


const { data: serverDate } = await useAsyncData("date", async () => {
    const date = dayjs().toString()
    await new Promise((resolve) => setTimeout(resolve, 2000))
    return date
});
</script>

<template>
    <button @click="count++">{{ count }}</button>
    <div class="box">
        <div>Server Date: {{ serverDate }}</div>
        <div>Client Date: {{ clientDate }}</div>
    </div>
</template>

<style scoped>
.hello {
    font-family: Arial, Helvetica, sans-serif;
    font-size: 3rem;
    padding: 10rem;
}
</style>