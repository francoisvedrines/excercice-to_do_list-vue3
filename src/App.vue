<script >

export default {
  data() {
    return {
      todos: [],
      newTodo: {}
    }
  },
  methods: {
    addTodo: function () {
      if (this.newTodo.text) {
        this.todos.push(this.newTodo);
        this.newTodo = {
          done: false
        };
        localStorage.setItem("todos", JSON.stringify(this.todos));
      }
      else {
        alert('champ non rempli');
      }
    },
    removeTodo: function (todo){
      const indexTodo = this.todos.findIndex((elem) => elem == todo);
      this.todos.splice(indexTodo,1);
    },
    removeAll: function (){
      confirm("Attention, toute la liste va être supprimée");
      this.todos = [];
    }
  },
  created() {
    this.todos = localStorage.getItem("todos") ? JSON.parse(localStorage.getItem("todos")) : this.todos;
  },
  updated() {
    localStorage.setItem("todos", JSON.stringify(this.todos));
  }
}
</script>

<template>

  <main>
  <section class="todo-list">

    <h3>To-do list de François</h3>

    <div class="all-todos" v-for="todo in todos">
      <div class="single-todo" :class="{ done: todo.done }">
        <p @click="todo.done = !todo.done">{{ todo.text }}</p>
        <button @click="removeTodo(todo)">&#10060;</button>
      </div>
    </div>


    <input type="text" placeholder="Ajouter un nouveau to-do" @keyup.enter="addTodo()" v-model="newTodo.text">
    <button class="add" @click="addTodo()">Ajouter</button>

    <div class="instructions">
      Instructions:
      <ul>
        <li>Utiliser le champ de saisie pour écrire un nouveau to-do et cliquer sur ajouter</li>
        <li>Cliquer sur le texte d'un to-do pour basculer à l'état de fait/à faire</li>
        <li>Utiliser le bouton croix à côté d'un to-do pour le supprimer</li>
        <li>Utiliser le bouton "Tout effacer" pour tout effacer </li>
      </ul>
    </div>

    <button class="clear" @click="removeAll()" v-if="todos.length">Tout effacer</button>
    
  </section>
  </main>
</template>

<style>
body {
  margin: 0;
  font-family: 'Open Sans', sans-serif;
}

main {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  flex-wrap: wrap;
  padding-top: 60px;
}

.todo-list input {
  box-sizing: border-box;
  height: 28px;
  border-radius: .25rem;
  width: 80%;
  border: 1px solid lightgrey;
  margin-top: 32px;
}

button {
  background-color: transparent;
  cursor: pointer;
  box-sizing: border-box;
  height: 28px;
  border-radius: .25rem;
  color: #fff;
}

button:hover {
  opacity: 0.8;
}

button.add {
  background-color: #007bff;
  border: 1px solid #007bff;
  margin-left: 2px;
}

button.clear {
  background-color: #dc3545;
  border: 1px solid #dc3545;
  display: block;
  margin: auto;
}

button:focus {
  outline: 0;
}

.todo-list h3 {
  text-align: center;
  margin-top: 24px;
  width: 100%;
}


.todo-list {

  flex-wrap: wrap;
  border: 1px solid lightgrey;
  background-color: rgb(248, 248, 248);
  padding: 40px;
  width: 900px;
  text-align: center;
  border-radius: .25rem;
}

.single-todo {
  display: flex;
  align-items: center;
  justify-content: space-around;

}

.single-todo p {
  margin: 12px 0;
  cursor: pointer;
}

.single-todo button {
  font-size: 8px;
  align-items: end;
  border: none;
}

.single-todo.done p {
  text-decoration: line-through;
}

.single-todo button.remove {
  width: 12px;
  height: 12px;
  border: none;
  background-size: contain;
  cursor: pointer;
  margin-left: 8px;
}

.todo-list button.clear {

  margin-top: 24px;
}

div.instructions {
  font-size: 11px;
  margin-top: 40px;
  color: grey;
}

div.instructions ul {
  list-style: inside;
  text-align: center;
  padding: 0;
}

div.instructions ul li {
  margin: 4px auto;
}
</style>
