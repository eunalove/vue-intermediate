<template>
  <div class="clearAllContainer">
    <span class= "clearAllBtn" v-on:click="clearTodo">Clear All</span>
  </div>
</template>

<script>
export default {

  methods: {
    clearTodo: function() {
      this.$emit('clearAll');
    }
  }

}
</script>

<style scoped>
.clearAllContainer {
  background-color: white;
  width: 8.5rem;
  height: 50px;
  line-height: 50px;
  margin: 0 auto;
}

.clearAllBtn {
  color: #62acde;
  cursor: pointer;
  font-weight: bold;
}

</style>