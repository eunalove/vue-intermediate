<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" @keyup.enter= "addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>
  </div>
</template>

<script>
export default {
    data: function(){
        return{
            newTodoItem: ""
        }
    },

    methods:{
      addTodo: function(){
        //저장하는 로직

        if(this.newTodoItem !== ''){
          this.$emit('addTodoItem',this.newTodoItem);
          this.clearInput();
        }
        
      },

      clearInput: function(){
        this.newTodoItem = '';
      }
    }
}
</script>

<style scoped>

</style>