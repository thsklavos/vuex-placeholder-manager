
<template>
<div>
  <h3>Todos</h3>
  <div class="legend">
    <span>Double click to mark as incomplete</span>
    <span>
      <span class="incomplete-box"></span> = Incomplete
    </span>
    <span>
       <span class="complete-box"></span> = Complete
    </span>
  </div>
  <div class="todos">
    <div @dblclick="onDblClick(todo)" v-for="todo in allTodos" :key="todo.id" class="todo" v-bind:class="{'is-complete':todo.completed}">
      {{todo.title}}
      <span @click="deleteTodo(todo.id)" class="trash"> &#9949;</span>
    </div>
  </div>
</div>
</template>

<script>
import{mapGetters,mapActions} from 'vuex'
export default {
name:'Todos',
methods:{
  ...mapActions(['fetchTodos','deleteTodo','updateTodo']),
  onDblClick(todo){
    const updTodo={
      id:todo.id,
      title: todo.title,
      completed:!todo.completed

    }
    this.updateTodo(updTodo);
  }
},
computed:mapGetters(['allTodos']),
created(){
  this.fetchTodos();
}
}
</script>

<style scoped>
.todos{
  display:grid;
  grid-template-columns:repeat(3, 1fr);
  grid-gap: 1rem
}

.todo{
  border:1px solid #ccc;
  background:#41b883;
  padding:1rem;
  border-radius: 5px;
  text-align: center;
  position:relative;
  cursor:pointer;
  font-weight:bold;
  -webkit-user-select: none;  /* Chrome all / Safari all */
  -moz-user-select: none;     /* Firefox all */
  -ms-user-select: none;      /* IE 10+ */
  user-select: none; 
}
.trash{
  cursor: pointer;
  position:absolute;
  right:5px;
  top:0;
}
.legend{
  display:flex;
  justify-content: space-around;
  margin-bottom: 1rem;
}
.complete-box{
  display:inline-block;
  width:10px;
  height:10px;
  background:#35495e;
}
.incomplete-box{
  display:inline-block;
  width:10px;
  height: 10px;
  background:#41b883;
}
.is-complete{
  background:#35495e;
  color:#fff;
}
@media(max-width:500px){
.todos{
  grid-template-columns: 1fr;
}
}

</style>