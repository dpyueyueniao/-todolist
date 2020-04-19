<template>
 <div class="edit_box col">
  <textarea
   class="text"
   type="text"
   v-model="newitem"
   >

  </textarea>
  <el-button 
   class="but" 
   @click="secNew"
  >
  确认修改
  </el-button> 
 </div>
 <!-- <el-dialog
    title="编辑框"
    width="42vw"
    :before-close="handleClose">
    <textarea 
     class="text"
     type="text"
     v-model="newitem"
    >
    </textarea>
    <span slot="footer" class="dialog-footer">
      <el-button
       @click="dialogOff"
      >取 消
      </el-button>
      <el-button 
       type="primary" 
       @click="secNew"
      >
      确 定
      </el-button>
    </span>
  </el-dialog> -->
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
  secNew: function() {
   this.$emit('secNew', this.index, this.newitem)
  }, 
  dialogOff: function() {
   this.$emit('dialogOff')
  }, 
  handleClose: function() {
   this.$emit('handleClose')
  }
 }
}
</script>

<style lang="less" scoped>
.edit_box{
 top: 30vh;
 position: fixed;
 .text{
  padding: 1rem;
  font-size: 1rem;
  width: 40vw; 
  height: 30vh;
  border-radius: .5rem;
 }
 .but{ 
  margin-top: 1rem;
  width: 8rem;
  height: 3rem;
  align-self: flex-end;
 }
}
</style>