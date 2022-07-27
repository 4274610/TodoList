<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo"></MyHeader>
        <List
          :todos="todos"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        ></List>
        <MyFooter
          :todos="todos"
          :checkallTodo="checkallTodo"
          :clearallTodo="clearallTodo"
        ></MyFooter>
      </div>
    </div>
  </div>
</template>
<script>
import MyHeader from "./components/MyHeader.vue";
import List from "./components/List.vue";
import MyFooter from "./components/MyFooter.vue";
export default {
  name: "App",
  components: {
    MyHeader,
    List,
    MyFooter,
  },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos"))||[]
      //从本地存储中获取数据,如果本地存储中没有内容，getItem得到的是null,那么后面相关的关于数组的属性就会报错，所以初始值给一个空数组
        // { id: "001", title: "吃饭", done: true },
        // { id: "002", title: "睡觉", done: false },
        // { id: "003", title: "打豆豆", done: true },
      
    };
  },
  methods: {
    //1、添加一个todo对象到todos
    addTodo(todoObj) {
      //接收子组件传过来的参数，把这个参数给放到数组里，形参可以随便写，但是为了看出来是哪里传过来的，最好一致
      this.todos.unshift(todoObj);
    },
    //2、勾选or取消勾选一个todo项
    checkTodo(id) {
      //id是Item里handleCheck传过来的id
      this.todos.forEach((item) => {
        //拿到的每一个todo项{ id: "001", title: "吃饭", done: true }
        if (item.id === id) {
          //如果触发change事件的那个id,就是这个item的id,那就表示触发的就是这个todo项，就给它取反
          item.done = !item.done;
        }
      });
    },
    //3、删除todo项
    deleteTodo(id) {
      //filter不改变原数组，所以需要把过滤出来的数组重新赋值给原数组
      this.todos = this.todos.filter((item) => {
        return item.id !== id;
      });
    },
    //4、总键控制上面的选项键是否全选
    checkallTodo(x) {
      //x传来的是true或false
      this.todos.forEach((item) => {
        item.done = x;
      });
    },
    //5、清除所有done值为真的选项
    clearallTodo() {
      this.todos = this.todos.filter((item) => {
        return !item.done;
      });
    },
  },
  watch: {   
    todos:{ 
      deep:true,
      handler(value){   
      localStorage.setItem("todos", JSON.stringify(value));
    }}
  },
};
</script>
<style>
body {
  background: #fff;
}
.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px (255, 255, 255, 0.2), 0 1px 1px (0, 0, 0, 0.6);
  border-radius: 4px;
}
.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}
.btn:focus {
  outline: none;
}
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
