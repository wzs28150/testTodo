<template>
  <section class="real-app">
      <input
        type = "text"
        class = "add-input"
        autofocus = "autofocus"
        placeholder="接下去要做什么?"
        @keyup.enter="addTodo"
      >
      <item
        :todo="todo"
        v-for="todo in filteredTodos"
        :key="todo.id"
        @del="deleteTodo"
        @update="updateTodo"
        @change="changeTodo"
        />
      <tabs :filter="filter"
      :todos="todos"
      @toggle="toggleFilter"
      @clearAllCompleted = "clearAllCompleted"
      />
  </section>
</template>
<script>
import Item from './item.vue'
import Tabs from './tabs.vue'
let id = 0

export default {
  data(){
    return{
      todos:[],
      filter:'all'
    }
  },
  components:{
    Item,
    Tabs,
  },
  computed:{
    filteredTodos(){
      if(this.filter === 'all'){
        return this.todos
      }
      const completed = this.filter === 'completed'
      return this.todos.filter(todo => completed === todo.completed)
    }
  },
  methods:{
    addTodo(e){
        this.todos.unshift({
          id: id++,
          content: e.target.value.trim(),
          completed:false,
          updated:false
        })
        e.target.value = ''
    },
    deleteTodo(id){
      this.todos.splice(this.todos.findIndex(todo => todo === id),1)
    },
    toggleFilter(state){
      this.filter = state
    },
    clearAllCompleted(){
      this.todos = this.todos.filter(todo => !todo.completed)
    },updateTodo(todo){
      todo.updated = todo.updated === true ? false : true
      // this.todo.updated = true
      // this.todo.content = this
    },changeTodo(todo){

      todo.updated = false
    }
  }
}
</script>
<style lang="stylus" scoped>
.real-app{
    width 600px
    margin :0px  auto
    box-shadow :0px 0px 5px #666
}
.add-input{
    positon:relative;
    margin 0px
    width 100%
    font-size 24px
    font-family  inherit
    font-weight:inherit
    line-height 1.4rem
    border 0;
    outline none
    color inherit
    padding 6px
    border 1px solid #999
    box-shadow: inset 0 -1px 5px 0px rgba(0,0,0,0)
    box-sizing border-box
    font-smoothing:antialiased;
    padding 16px 16px 16px 60px
    border none
}
</style>
