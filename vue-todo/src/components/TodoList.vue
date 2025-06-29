<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item">
        <i class="fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}"
        v-on:click="toggleComplete(todoItem)"></i>
        
        <span v-bind:class= "{textCompleted: todoItem.completed}">{{ todoItem.item }}</span> 
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['propsdata'],

  methods:{
    removeTodo: function(todoItem, index){

      this.$emit('removeTodoItem', todoItem, index);
    },

    toggleComplete: function(todoItem){
      todoItem.completed =! todoItem.completed;
      //로컬 스토리지의 데이터 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    }
    
  },

}
</script>

<style scoped>

.checkBtn{
  color: #62acde;
  margin-right: 5px;
}

.checkBtnCompleted {
  color: #b4adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
</style>