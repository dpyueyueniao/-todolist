<template>
 <div class="popbox">
  <p class="yn">
   是否确认删除
  </p>
 <div class="row popbutbox">
  <button @click="popY">确认</button>
  <button @click="popN">取消</button>
 </div>
 </div>
</template>

<script>
export default {
 name: 'popup', 
 methods: {
  popY () {
   this.$emit('popY')
  }, 
  popN () {
   this.$emit('popN')
  }
 }
}
</script>


<style lang="less" scoped>
  .popbox{
   padding: .5rem;
   width: 15vw;
   height: 10vh;
   border: .2rem solid #000;
   border-radius: .5rem;
   position: fixed;
   top: 40vh;
   background: rgba(238, 238, 238, 0.911);
   .popbutbox{
    margin-top: 1rem;
    justify-content: space-around;
   }
   .yn{
    font-size: 1.5rem;
    color: rgb(218, 12, 12);
   }
 }
 
 
</style>