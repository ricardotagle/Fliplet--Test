<div id="app">
  <h2>To do: ({{ todos.length }})</h2>
  <input 
    v-model="newTodo" 
    @keyup.enter="addTodo" 
    type="text" 
    placeholder="Type something and press ENTER"
  />
  
  <ol>
    <li v-for="(todo, index) in todos" :key="index">
      <label>
        <input type="checkbox" @change="markAsCompleted(index)" />
        <span>{{ todo.text }}</span>
        <a href="#" class="remove" @click.prevent="removeTodo(index)">Remove</a>
      </label>
    </li>
  </ol>
  
  <hr />
  
  <h2>Completed items: ({{ completed.length }})</h2>
  
  <ol>
    <li v-for="(todo, index) in completed" :key="'c-' + index">
      <label>
        <input type="checkbox" checked @change="markAsTodo(index)" />
        <span class="line-through">{{ todo.text }}</span>
        <a href="#" class="remove" @click.prevent="removeCompleted(index)">Remove</a>
      </label>
    </li>
  </ol>
</div>

<script>
new Vue({
  el: "#app",
  data: {
    newTodo: "",
    todos: [
      { text: "Learn about Vue" },
      { text: "Learn about Fliplet" },
      { text: "Play around in JSFiddle" },
      { text: "Show us what you've got" }
    ],
    completed: [
      { text: "Send job application" }
    ]
  },
  methods: {
    // Adds a new task to the list
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({ text: this.newTodo.trim() });
        this.newTodo = ""; // Clear input field
      }
    },

    // Moves a task from "To do" to "Completed"
    markAsCompleted(index) {
      this.completed.push(this.todos[index]);
      this.todos.splice(index, 1);
    },

    // Moves a task from "Completed" back to "To do"
    markAsTodo(index) {
      this.todos.push(this.completed[index]);
      this.completed.splice(index, 1);
    },

    // Removes a task from the "To do" list
    removeTodo(index) {
      this.todos.splice(index, 1);
    },

    // Removes a task from the "Completed" list
    removeCompleted(index) {
      this.completed.splice(index, 1);
    }
  }
});
</script>

<style>
body {
  background: #20262E;
  padding: 20px;
  font-family: Helvetica, Arial, sans-serif;
  color: white;
}

#app {
  background: #fff;
  border-radius: 4px;
  padding: 20px;
  transition: all 0.2s;
  color: black;
}

h2 {
  font-weight: bold;
  margin-bottom: 15px;
}

li {
  margin: 8px 0;
}

input[type="text"] {
  padding: 10px;
  width: 200px;
}

label .remove {
  display: none;
  color: red;
}

label:hover .remove {
  display: inline-block;
  margin-left: 10px;
  opacity: 0.6;
}

.remove {
  color: red;
  margin-left: 10px;
  cursor: pointer;
}

.line-through {
  text-decoration: line-through;
  color: gray;
}
</style>
