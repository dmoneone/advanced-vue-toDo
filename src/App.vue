<template>
  <div id="app">
   <h1>To Do List App</h1>
   <addItem v-on:add-item="addItem"/>
   <hr>
   <select v-model="filtered">
      <option value="All">All</option>
      <option value="Not-completed">Not-completed</option>
      <option value="Completed">Completed</option>
   </select>
   <hr>
   <todoList
      v-if="filterList.length"
      v-bind:todos="filterList"
      v-on:remove-todo="removeItem"
      v-on:save-todo="saveTodo"
   />
   <p v-else>No todos !</p>
  </div>
</template>

<script>
    import todoList from '@/components/todoList.vue';
    import addItem from '@/components/addItem.vue';
    export default {
      name: 'app',
      components: {
        todoList,addItem
      },
      data() {
          return {
              todos: [
                  {id: 1,title: 'go home',completed: true},
                  {id: 2,title: 'go for a walk',completed: false}
              ],
              filtered: 'All'
          }
      },
      computed: {
        filterList() {
          switch (this.filtered) {
            case 'All':
              return this.todos;
              break;
            case 'Completed':
              return this.todos.filter(t=>t.completed);
              break;
            case 'Not-completed':
              return this.todos.filter(t=>!t.completed);
              break;
          }
        }
      },
      methods: {
          removeItem(id) {
              this.todos = this.todos.filter(t => t.id !== id)
          },
          saveTodo(i,retitle) {
              this.todos[i].title = retitle;
          },
          addItem(item) {
             console.log(item)
             this.todos.push(item)
          }
      }
    }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


</style>
