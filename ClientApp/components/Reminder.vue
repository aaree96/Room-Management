<template>
    <UModal
        title="Reminder"
>
    <template #body>
        <ol class="list-inside list-decimal">
            <li v-for="event in events" :key="event">
                <b>{{ event.name }}<br/></b>
                <div class="ml-12">Event: {{ event.name }}
                Start: {{ new Date(event.startAt).toLocaleTimeString() }} - End: {{ new Date(event.endAt).toLocaleTimeString() }}<br/>
                Room: {{ event.roomId }}</div>
            </li>
        </ol>
    </template>
</UModal>        
</template>

<script setup lang="ts">
const events = ref()

let currentDate = new Date()

$fetch(`/api/v1/Event/Events?start=${currentDate.toLocaleDateString()}&end=${currentDate.toLocaleDateString()}`, {
    server: false,
    headers: {
        authorization: `Bearer ${localStorage.getItem('token')}`
    },
    onResponse({ response }) {
        events.value = response._data
    }
})
</script>