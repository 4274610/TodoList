<template>
  <div class="todo-footer" v-show="total">
    <!--total为 0是false，就可以隐藏 -->
    <label>
      <!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>已经完成{{ doneTotal }}</span
      >/全部{{ total }}</span
    >
    <button class="btn btn-danger" @click="clearAll">清除已完成的任务</button>
  </div>
</template>

<script scoped>
export default {
  name: "MyFooter",
  props: ["todos", "checkallTodo", "clearallTodo"],
  computed: {
    total() {
      return this.todos.length;
    },
    // reduce两个参数(函数(pre,current)，统计的初始值)数组的长度是几，函数就会被调几次
    // pre：上一次函数的返回值，就是这一次的pre值
    // current:每一个todo项
    // 最后一个返回值，就是函数的返回值
    doneTotal() {
      return this.todos.reduce((pre, todo) => pre + (todo.done ? 1 : 0), 0);
    },
    //1、上面的选项是否全选，控制总键是否全选
    isAll: {
      get() {
        return this.doneTotal === this.total && this.total > 0; //返回值是布尔值，所以value也是布尔值
      },
      // 2、总键控制上面的选项键是否全选,方式二
      set(value) {
        console.log(value);
        this.checkallTodo(value); //输出的是true或false
      },
    },
  },
  //2、总键控制上面的选项键是否全选,方式一
  //如果checkAll是true,todo项都是true,通知APP总键是否全选
  methods: {
    //methods可以传参
    // checkAll(e){
    //   this.checkallTodo(e.target.checked)//输出的是true或false
    //   console.log(e.target.checked);
    // }
    //3、通知APP清除所有done值为真的选项
    clearAll() {
      if (confirm("确定删除吗？")) {
        this.clearallTodo();
      } //直接调用，不用传值
    },
  },
};
</script>

<style scoped>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}
.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}
.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}
.todo-footer button {
  float: right;
  margin-right: 5px;
}
</style>
