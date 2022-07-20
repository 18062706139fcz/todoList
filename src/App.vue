<script setup lang="ts">
// setup是干嘛的？
// 内联渲染，无需注册，直接使用
// 需要引入Vue中的computed onMounted ref
import {computed,onMounted,ref} from 'vue';
// 定义相关变量｜todo｜todoList
let inputValue = ref<string>("");
type Todo = {
  value: string,
  done: boolean
};
let todoLists = ref<Todo[]>([
  { value: 'Ryker想吃饭饭', done:false},
  { value: 'Ryker想拿牌牌', done:true},
  { value: 'Ryker想打人人', done:false},
]);
const handleAdd = () => {
  if (inputValue.value) {
    const list:Todo = { value:inputValue.value, done:false};
    todoLists.value.push(list);
    inputValue.value = '';
  }

};
// 
const handleRemove = (index: number) => {
  todoLists.value.splice(index, 1);
};
// remove
const handleClear = () => {
  todoLists.value = todoLists.value.filter((item) => !item.done)
};
// const selectAll = (f:boolean) => {
//   todoLists.value.forEach((item) => {
//     item.done = f;
//   })
// }
// let ano:boolean = false;
// const Judge = () => {
//   selectAll(!ano)
//   ano = !ano
// }
const active = computed(() => {
  return todoLists.value.filter((item) => item.done).length
});
const all = computed(() => {
  return todoLists.value.length;
});
// const fix = () => {
//   if(active.value === all.value - 1) {
//     ano = true;
//     selectAll(!ano);
//   } else if (active.value === 1) {
//     ano = false;
//     selectAll(!ano)
//   }
// };
const isAllDone = computed({
  get() {
    return active.value == all.value;
  },
  set(value: boolean) {
    return todoLists.value.forEach((item) => item.done = value)
  }
})
const input = ref(null);
</script>

<template>
<div class="container">
    <input 
    ref="input"
    type="text" 
    class="styled"
    v-model="inputValue"
    >
    <button @click="handleAdd">add</button>
    <button @click="handleClear">remove</button>
    <ul v-if="todoLists.length">
    <li
    v-for="(todo, index) in todoLists"
    :key="index"
    :class="{done: todo.done}"
    >
    <input type="checkbox" v-model="todo.done" />
    {{ todo.value }}
    </li>
    <span>全选</span><input type="checkbox" v-model="isAllDone"/>
    {{ `${active}/${all}` }}
    </ul>
    <div v-else>nothing here</div>
</div>
</template>

<!-- container实现了垂直居中 -->

<style scoped>
.container {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    width: 400px;
}
li {
  text-align: left;
}
span {
  text-align: left;
}
.done {
  text-decoration: line-through;
}
</style>
