<template>
  <div id="app">
    <hr />
    <button type="button" class="btn btn-primary btn-lg">Large button</button>
    <hr />
    <Chart></Chart>
    <hr />
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>

</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput  from './components/TodoInput.vue'
import TodoList   from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'
import Chart      from './Chart.vue'

export default{
  name :'app',
  data(){
     return{
       todoItems : [],
       msg : 'Welcome to Your Vue.js App'
     }
   },


   methods:{
     clearAll(){
       localStorage.clear();
       this.todoItems = [];
     },
     addTodo(todoItem){
          localStorage.setItem(todoItem,todoItem);
          this.todoItems.push(todoItem);
     },
     removeTodo(todoItem,index){
       localStorage.removeItem(todoItem);
       this.todoItems.splice(index,1);
        //console.log(todoItem,index);
     }
   },
   created(){
     if(localStorage.length > 0){
       for(var i=0; i<localStorage.length;i++){
         this.todoItems.push(localStorage.key(i));
       }
     }
   },
   components : {
     'TodoHeader' : TodoHeader,
     'TodoInput'  : TodoInput,
     'TodoList'   : TodoList,
     'TodoFooter' : TodoFooter,
      Chart
   }

}


</script>

<style>
body {
  text-align : center;
  background-color:  #F6F6F8;
}

input {
  border-style:  groove;
  width : 200 px;
}

button {
  border-style : groove;
}

.shadow {
  box-shadow : 5px 10px 10px rgba(0, 0, 0, 0.03);
}

</style>
