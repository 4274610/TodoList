<template>
  <li>
    <label
      ><input
        type="checkbox"
        :checked="todo.done"
        @change="handleCheck(todo.id)"
      /><span>{{ todo.title }}</span></label
    >
    <!-- :checked="todo.done" 初始化显示之前的勾选和未勾选-->
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
  </li>
</template>

<script>
export default {
  name: "Item",
  props: ["todo", "checkTodo", "deleteTodo"], //数据接收,加引号
  methods: {
    //勾选
    handleCheck(id) {
      //输出传参传过来的id
      // console.log(id);
      //数据在哪里 ，就在哪里操作数据，这里的数据在APP里，
      //通过调用函数的方式，子组件通过传参把这个id传给父组件，
      //让父组件接收到参数，通知App组件将id对应的todo对象的done值取反
      this.checkTodo(id);
    },
    //删除
    handleDelete(id) {
      //通知App组件id删除对应的todo项
      if (confirm("确定删除吗？")) {
        this.deleteTodo(id);
      }
    },
  },
};
</script>

<style sxoped>
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}
li label {
  float: left;
  cursor: pointer;
}
li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}
li .btn {
  float: right;
  display: none;
  margin-top: 3px;
}
li:before {
  content: initial;
}
li:last-child {
  border-bottom: none;
}
li:hover {
  background-color: rgb(198, 197, 197);
}
li:hover button {
  display: block;
}
</style>
