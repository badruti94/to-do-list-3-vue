<script setup>
import List from '@/components/List.vue';
import {API} from '../config/api'
import { onMounted, ref } from 'vue';


const todo = ref([])
const text = ref('')

const fetchData = async () => {
  try {
    const result = await API.get('/todo')

    todo.value = result.data.data
  } catch (error) {
    console.log(error);
  }
}

onMounted(() => {
  fetchData()
})

const onSubmit = async () => {
  try {
    await API.post('/todo', { todo: text.value })
    fetchData()
  } catch (error) {
    console.log(error);
  }
}

const onDone = async (id) => {
  try {
    await API.patch(`/todo/${id}/done`)
    fetchData()
  } catch (error) {
    console.log(error);
  }
}

const onDelete = async (id) => {
  try {
    await API.delete(`/todo/${id}`)
    fetchData()

  } catch (error) {
    console.log(error);
  }
}

</script>

<template>
  <div class="w-2/4 mx-auto my-10">
    <form action="" @submit.prevent="onSubmit">
      <input id="text" class="w-full px-5 py-3 outline-none border-2 border-gray-400 rounded-lg text-lg box-border"
        type="text"
        v-model="text"
        >
    </form>
    <div class="mt-12 w-full">
      <List
      v-for="td in todo" 
      :key="td._id"
      :id="td._id"
      :todo="td.todo"
      :done="td.done"
      @onDone="onDone(td._id)"
      @onDelete="onDelete(td._id)"
      />
    </div>
  </div>
</template>
