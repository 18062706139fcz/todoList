
<script setup lang="ts">
import { computed, onMounted, ref } from "vue";
let inputValue = ref<string>("");
type Todo = {
  titile: string;
  isDone: boolean;
};
let todoList = ref<Todo[]>([
  { titile: "速冻鱼吃饭", isDone: false },
  { titile: "速冻鱼睡觉", isDone: false },
  { titile: "速冻鱼学习vue3", isDone: true },
]);
const handlerAdd = () => {
  if (inputValue.value) {
    const todo: Todo = { titile: inputValue.value, isDone: false };
    todoList.value.push(todo);
    inputValue.value = "";
  }
};
const input = ref(null);
onMounted(() => {
  if (input.value !== null)
    // @ts-ignore
    input.value.focus();
});
</script>

<template>
  <div class="container">
    <input
      ref="input"
      type="text"
      v-model="inputValue"
    />
    <button @click="handlerAdd">add</button>
    <button >clear</button>
    <ul v-if="todoList.length">
    </ul>>
  </div>
</template>

<style>
.container {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.done {
  text-decoration: line-through;
}
</style>