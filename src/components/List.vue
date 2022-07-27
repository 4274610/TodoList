<template>
  <ul class="todo-main">
    <Item v-for="todoObj in todos" :key="todoObj.id" :todo="todoObj" :checkTodo="checkTodo" :deleteTodo="deleteTodo"></Item>
    <!-- 组件之间传数据用props,把todoObj传过去
        todo是用于另一个组件接收，可以随便取名字 -->
  </ul>
</template>

<script>
import Item from "./Item";
export default {
  name: "List",
  components: { Item },
  props:["todos","checkTodo","deleteTodo"]//vm传给vc，vc接收
};
</script>

<style scoped>
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}
.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>
