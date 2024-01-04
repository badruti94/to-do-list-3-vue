<script setup>
defineProps({
    id: String,
    todo: String,
    done: Boolean,
})
</script>
<template>
    <div 
    class="todo w-full flex justify-between rounded-lg mb-4 px-2 py-1"
    :class="{ 'bg-green-800' : done, 'bg-gray-500' : !done  }"
    >
        <p class="todo-text text-xl">{{ todo }}</p>
        <div class="flex flex-col justify-around">
            <div 
            class="py-3 px-8 rounded-lg text-xs cursor-pointer text-white bg-green-500"
            @click="$emit('onDone')"
            >done</div>
            <div class="py-3 px-8 rounded-lg text-xs cursor-pointer text-white bg-red-500"
            @click="$emit('onDelete')"
            >delete</div>
        </div>
    </div>
</template>