<template>
  <div class="todo-header">
    <input
      type="text"
      placeholder="请输入你的任务名称，按回车键确认"
      @keyup.enter="add"
      v-model="title"
    />
  </div>
</template>

<script>
import { nanoid } from "nanoid";
export default {
  name: "MyHeader",
  data() {
    return {
      title: "",
    };
  },
  props: ["addTodo"],
  // 子组件给父组件传东西：父组件先传给子组件一个函数，子组件接收后，去传参调用，父组件就能接收到这个参数
  methods: {
    add() {
      //1、校验数据：空格、不输入内容都不能添加上
      if (!this.title.trim()) return alert("不能为空"); //if(!this.title.trim())return //如果为空就结束逻辑
      //2、把用户输入的内容包装成一个数组，然后加到list的数组里
      const todoObj = { id: nanoid(), title: this.title, done: false }; //如果上面不绑定v-model="title"，就写e.target.value 参数写e
      //3、通知App组件添加新输入的数据
      this.addTodo(todoObj); //子组件接收父组件传过来的函数后，去传参调用，让父组件接收到参数
      //4、清空输入
      this.title = "";
    },
  },
};
</script>

<style scoped>
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}
.todo-header input:focus {
  outline: none;
  /* border-color:(82,168,236,0.8) ; */
  border-color: red;
  background-color: antiquewhite;
  box-shadow: inset 0 1px (0, 0, 0, 0.075), 0 0 8px (82, 168, 236, 0.6);
}
</style>
