<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput></TodoInput>
    <TodoInput v-on:addTodoItem= "addOneItem"></TodoInput>
    <TodoList v-bind:propsdata= "todoItems" v-on:removeTodoItem= "removeOneItem"
    v-on:removeItem="toggleOneItem"></TodoList>
    <TodoFooter></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {

  data: function() {
    return {
      todoItems: []
    }
  },

  methods: {
    addOneItem: function(todoItem){
      
        var obj= {completed: false, item: todoItem};
        localStorage.setItem(todoItem, JSON.stringify(obj));
        this.todoItems.push(obj);
    },

    removeOneItem: function(todoItem, index) {
      // 로컬 스토리지에서 아이템 제거
      localStorage.removeItem(todoItem.item);
      // todoItems 배열에서 아이템 제거
      this.todoItems.splice(index, 1);
    },

    toggleOneItem: function(todoItem, index) {
      //todoItem.completed =! todoItem.completed;
      this.todoItems[index].completed = !this.todoItems[index].completed
      //로컬 스토리지의 데이터 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    } 
  },
  

  
    created: function() {
      if (localStorage.length > 0) {
        for (var i = 0; i < localStorage.length; i++) {
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
      }
    },


  components:{
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  }
}
</script>

<style>
body{
  text-align: center;
  background-color: #F6F6F6;
}
input{
  border-style: groove;
  width: 200px;
}

button{
  border-style: groove;
}

.shadow{
  box-shadow: 5px 10px 10px rgb(0,0,0,0.03);
}
</style>
