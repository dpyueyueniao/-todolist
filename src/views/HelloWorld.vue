<template>
  <div class="home_box">
    <div class="col home">
      <h1 class="title">鹏神的第二个Todolist</h1>
      <div class="search row">
        <!-- <input class="ipt" type="text" v-model="ipt_content"/> -->
        <el-input
          class="ipt"
          placeholder="请输入内容"
          v-model="ipt_content"
          clearable>
        </el-input>
        <el-button
         class="but" 
         @click="handelNewList"
         type="primary"
        >
        提交
        </el-button>
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
        :visible.sync="itemadd"
        v-if="sec.show"
        :new_content="sec.new_content"
        :index="sec.index"
        :key="compileKey"
        @secNew="secNew"
      >
      </Compile>
  </div>
  </div>
</template>

<script>
import TodoItem from '../components/TodoItem.vue'
import Compile from '../components/Compile.vue'

export default {
  name: 'HelloWorld', 
  components: {
    TodoItem, 
    Compile,
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
        this.$alert('内容不能为空')
      }
    },
    itemdel: function(index) {
      this.$confirm('是否确认删除', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.todolist.splice(index, 1), 
          localStorage.setItem('todolist', JSON.stringify(this.todolist))
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
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
    }
    // dialogOff: function() {
    //   this.sec.show = false
    // },
    // handleClose: function() {
    //   this.sec.show = false
    // }
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
  background: rgb(236, 255, 206);
    .title{
    margin: 3rem 0 3rem;
    font-size: 1.5rem;
    color: rgb(59, 55, 0);
  }
  .search{
    width: 50vw;
    margin-bottom: 2rem;
    justify-content: space-between;
    .ipt{
      width: 44vw;
      height: 2rem;
    }
    .but{
      width: 5vw;
    }
  }
  .content{
    font-size: 1rem;
    width: 50vw;
    margin: 1rem 0 1rem;
    padding: 0 2rem 0;
    height: 3.5rem;
    line-height: 3.5rem;
    border-radius: .5rem; 
    justify-content: space-between;
  }
  .bg{
    position: fixed;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, .5);
  }
}



</style>
