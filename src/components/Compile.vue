<template>
 <div class="edit_box col">
  <textarea class="text" v-model="newitem"></textarea>
  <button class="but" @click="newright">确认修改</button> 
 </div>
</template>

<script>
export default {
 name: "Compile", 
 props: [
  'new_content', 
  'index'
 ], 
 created () {
  this.newitem = this.new_content
 }, 
 data () {
  return{
   newitem: ''
  }
 }, 
 methods: {
  newright: function() {
   this.$emit('secNew', this.index, this.newitem)
  }
 }
}
</script>

<style lang="less" scoped>
.edit_box{
 top: 30vh;
 width: 40vw;
 height: 30vh;
 border-radius: 1rem;
 position: fixed;
 background-color: rgba(134, 134, 134, 0.87);
 .text{
  padding: 1rem;
  font-size: 1rem;
  width: 100% - 4.4rem;
  height: 100%;
  resize: none;
  border-radius: 1rem;
 }
 .but{
  cursor: pointer;  
  margin: 1rem;
  width: 8rem;
  height: 3rem;
  border-radius: .3rem;
  background-color: #dcdcdc;
  align-self: flex-end;
 }
}
</style>