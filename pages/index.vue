<template>
  <div>
    <h1>Index Page</h1>
    <!-- 组件自动导入 -->
    <BaseFooButton />
    <!-- 组件懒加载 -->
    <h1>Mountains</h1>
    <LazyMountainsList v-if="show" />
    <button
      v-if="!show"
      @click="show = true"
    >
      显示列表
    </button>

    <!-- 待办列表 -->
    <div
      v-for="todo in todos"
      :key="todo.id"
    >
      <input
        v-model="todo.completed"
        type="checkbox"
      >
      <strong>{{ todo.title }}</strong>
    </div>

    <button @click="counter++">
      +
    </button>
    {{ counter }}
    <button @click="counter--">
      -
    </button>

    <NuxtLink to="/detail">
      Detail
    </NuxtLink> |
    <NuxtLink to="/user-admin/1">
      /user-admin/1
    </NuxtLink> |
    <NuxtLink to="/parent">
      /parent/child
    </NuxtLink> |
    <NuxtLink to="/helloworld">
      /helloworld
    </NuxtLink> |
  </div>
</template>
<script setup>
import { ref } from 'vue';
const show = ref(false);

// useAsyncData使用
const { data: todos } = await useAsyncData('todos', () => $fetch('/api/todo'), {
  transform(input) {
    return input.data
  },
  // pick: ['data'],
})
console.log(todos.value)
// useFetch使用
// const { data: todos } = await useFetch("/api/todo", {
//   // pick: ["id", "title", "completed"],
// });

// 声明SSR友好的状态
const counter = useCounter()
</script>
