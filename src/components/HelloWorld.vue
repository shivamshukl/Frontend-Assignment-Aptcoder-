<template>
    
  
  <div>
    <ul class="inst">
      <li class="nn">
        Click on the task to mark it as Done!
      </li>
      <li class="nn">
        Press Enter to add new Task!
      </li>
      <li class="nn">
        Press Delete to Remove Task from List!
      </li>
    </ul>
    
    <h1>Todo List </h1>
    <input
      type="text"
      v-model="todoName"
      @keyup.enter="addTodo"
      aria-label="Add a new Todo"
      placeholder="Add a new Todo"
    />
   
    <ul>

      <li 
        v-for="todo of todos"
        :class="{ done: todo.done }"
        :key="todo.id"
        @click="doneTodo(todo.id)"
        
      >
      {{todo.name }}({{ todo.date }}) 
      <button @click="removeTodo(todo.id)">Delete</button>
      <br><br>
      </li>
      </ul> 
      <p class="detail">Designed by Shivam Shukla with ❤</p>
  </div>

 
</template>


<script>


import axios from "axios";
const baseURL = "http://localhost:3001/todos";
export default {
  name: "TodoList",
  data() {
    return {
      todos: []
    };
  },
  async created() {
    try {
      const res = await axios.get(`http://localhost:3001/todos`);

      this.todos = res.data;
    } catch (e) {
      console.error(e);
    }
  },
  
  methods: {
    async addTodo() {
      try {
        
       var dt = new Date();
      const dispdate=dt.getFullYear() + "/" + (dt.getMonth() + 1) + "/" + dt.getDate();


      const res= await axios.post(baseURL, 
	{ 
		name: this.todoName, 
		date: dispdate
	})

        this.todos = [...this.todos,res.data];

        this.todoName = "";
        
      } catch (e) {
        console.error(e);
      }
    },
    async removeTodo(get) {
      try {
        await axios.delete(`${baseURL}/${get}`)
      } catch (e) {
        console.error(e);
      }
    }
    ,
    async doneTodo(id) {
  try {
    await axios.patch(`${baseURL}/${id}`, {
      done: true
    });

    this.todos = this.todos.map(todo => {
      if (todo.id === id) {
        todo.done = true;
      }

      return todo;
    });
  } catch (e) {
    console.error(e);
  }
}
  }
};
</script>

<style scoped>
 
h1 {
  text-decoration: underline;
  color:black;
}

li {
  color:white ;

}
.done {
  text-decoration: line-through;
  
}
.nn
{
  font-size: 30px;
  color: black;
  font-weight: 700;
}
.inst{
 position: relative;
 left:650px;
 top: 210px;
}
.detail{
  position: relative;
  left: 690px;
  top: 0px;
  color:black;
  font-weight: 700;
  border: 2px solid;
  background-color:darkgreen;
}

</style>
