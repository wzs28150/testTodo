<template>
  <div :class="['todo-item',todo.completed?'conpleted':'']">
    <input
        type="checkbox"
        class="toggle"
        v-model="todo.completed"
    >
    <label v-if="todo.updated == false">{{ todo.content}}</label>
    <label v-else><input type="text" class="add-input"  v-model="todo.content" @keyup.enter="changeTodo" ></label>
    <button class="update" @click="updateTodo">update</button>
    <button class="destroy" @click="deleteTodo"></button>
  </div>
</template>

<script>
export default {
  props:{
      todo:{
          type:Object,
          required: true,
      }
  },
  methods:{
      deleteTodo(){
        this.$emit('del',this.todo.id)
      },updateTodo(){
        this.$emit('update',this.todo)
      },changeTodo(e){
        this.$emit('change',this.todo)
      }
  }
}
</script>
<style lang="stylus" scoped>
.todo-item
  position relative
  background #ffffff
  font-size 24px
  border-bottom 1px solid rgba(0,0,0,.06)
  &:hover
    .destroy:after {
         content: 'x'
    }

  label
    white-space pre-line
    word-break break-all
    padding 15px 60px 15px 15px
    margin-left 45px
    display block
    line-height 1.2
    transition color 0.4s
&.completed{
    label
    color #d9d9d9
    text-decoration line-through
}
.toggle{
  text-align center
  width 40px
  height 40px
  position absolute
  top 0
  bottom 0
  margin auto 0
  border none
  outline none
  appearance none
}
  .toggle:before{
    content:url('../assets/images/round.png')
    position absolute
    left 12px
    cursor pointer
  }
  .toggle:checked:before{
    content : url('../assets/images/done.png')
    position absolute
    left 12px
    cursor pointer
  }
.destroy
  position absolute
  top 50%
  right 10px
  bottom 0;
  width 40px
  height 40px
  margin auto 0;
  font-size 30px
  color #cc9a9a;
  margin-bottom 11px
  transition: color 0.2s east-out
  background-color transparent
  appearance none
  border-width 0
  cursor pointer
  outline none
.update
    position absolute
    top 50%
    right 30px
    bottom 0;
    width 4em
    height 40px
    margin auto 0;
    font-size 30px
    color #cc9a9a;
    margin-bottom 11px
    transition: color 0.2s east-out
    background-color transparent
    appearance none
    border-width 0
    cursor pointer
    outline none
.add-input{
        margin 0px
        width 150px
        font-size 24px
        font-family  inherit
        font-weight:inherit
        line-height 38px
        border 0;
        outline none
        color inherit
        border 1px solid #999
        box-shadow: inset 0 -1px 5px 0px rgba(0,0,0,0)
        box-sizing border-box
        font-smoothing:antialiased;

        border none
    }
</style>
