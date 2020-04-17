<template>
 <div class="list_box">
  <p class="content">{{todo_item}}</p>
  <div>
   <span class="todo_but" @click="todoitemAdd">编辑</span>
   <span class="todo_but" @click="todoitemDel">删除</span>
  </div>
 </div>
</template>

<script>
export default {
 name: 'TodoItem', 
 props: [
  'todo_item', 
  'index'
 ], 
 methods: {
  todoitemDel: function() {
   this.$emit('itemdel', this.index)
  }, 
  todoitemAdd: function() {
   this.$emit('itemadd', this.index, this.todo_item)
  }
 }
}
</script>

<style lang="less" scoped>
 .todo_but{
  margin: 1rem;
  cursor: pointer
 }
</style>