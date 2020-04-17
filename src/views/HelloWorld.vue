<template>
  <div class="home_box">
    <div class="col home">
      <h1 class="title">鹏神的第二个Todolist</h1>
      <div class="search">
        <input class="ipt" type="text" v-model="ipt_content"/>
        <button class="but" @click="handelNewList">提交</button>
      </div>
      <TodoItem class="content row"
        :todo_item = "todo_text"
        v-for="(todo_text, index) in todolist"    
        :key="index"
        :index="index"
        @itemdel="itemdel"
        @itemadd="itemadd"
      >
      </TodoItem>
      
      <div
        class="bg"
        v-show="bg_show"
        @click="bg_click"
      >
      </div>
      <Compile 
        v-if="sec.show"
        :new_content="sec.new_content"
        :index="sec.index"
        :key="compileKey"
        @secNew="secNew"
      >
      </Compile>
      <popup
        v-if="pop.show"
        :key="popKey"
        @popY="popY"
        @popN="popN"
      >
      </popup>
  </div>
  </div>
</template>

<script>
import TodoItem from '../components/TodoItem.vue'
import Compile from '../components/Compile.vue'
import popup from '../components/popupwindows.vue'

export default {
  name: 'HelloWorld', 
  components: {
    TodoItem, 
    Compile,
    popup
  }, 
  data () {
    return {
      ipt_content: '', 
      todolist: JSON.parse(localStorage.getItem('todolist')) || [], 
      sec: {
        show: false,
        index: NaN,
        new_content: '' 
      }, 
      pop: {
        show: false
      }, 
      bg_show: false
    }
  }, 
  methods: {
    handelNewList: function() {
      if(this.ipt_content){
        this.todolist.push(this.ipt_content), 
        localStorage.setItem('todolist', JSON.stringify(this.todolist)), 
        this.ipt_content = ''
      }else{
        alert('内容不能为空')
      }
    },
    itemdel: function() {
      this.pop.show = true
      this.bg_show = true
    }, 
    itemadd: function(i, newitem){
      this.bg_show = true
      this.sec.show = true
      this.sec.index = i
      this.sec.new_content = newitem
      this.compileKey = Math.random()
    }, 
    secNew: function(i, newitem) {
      this.todolist.splice(i, 1, newitem)
      this.bg_show = false
      this.sec.show = false
      localStorage.setItem('todolist', JSON.stringify(this.todolist))
    }, 
    bg_click: function() {
      this.bg_show = false
      this.sec.show = false
      this.pop.show = false
    }, 
    popY: function(index) {
      this.todolist.splice(index, 1), 
      this.pop.show = false
      this.bg_show = false
      localStorage.setItem('todolist', JSON.stringify(this.todolist))
    }, 
    popN: function() {
      this.pop.show = false
      this.bg_show = false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
.home{
  width: 100%;
  align-items: center;
  text-align: center;
  min-height: 100vh;
  background: rgb(206, 255, 247);
    .title{
    margin: 3rem 0 3rem;
    font-size: 1.5rem;
    color: rgb(59, 55, 0);
  }
  .search{
    width: 100%;
    margin-bottom: 2rem;
    .ipt{
      width: 44%;
      height: 2rem;
    }
    .but{
      width: 5%;
      cursor: pointer;  
      margin-left: 1rem;
      width: 6rem;
      height: 2.6rem;
      border-radius: .3rem;
    }
    .but:hover {
        background-color: rgba(148, 150, 151, 0.651); 
        border: 1px solid #0F0F0F;
        color: white;
    }
  }
  .content{
    margin: 1rem 0 1rem;
    padding: 0 3rem 0;
    height: 3rem;
    line-height: 3rem;
    width: 60rem;
    background: rgba(252, 255, 62, 0.5);
    border-radius: .5rem; 
    justify-content: space-between;
  }
  .bg{
    position: fixed;
    width: 100vw;
    height: 100vh;
    background-color: rgba(241, 243, 148, 0.226);
  }
}



</style>
