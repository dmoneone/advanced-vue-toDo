<template>
    <div>
      <button v-on:click="isEdited = !isEdited">
        <span v-if="!isEdited">Edit</span>
        <span v-else>Hide editing</span>
      </button>
       <ul>
        <todoItem
           v-bind:isEdited="isEdited"
           v-for="(todoItem,index) in todos"
           v-bind:todoItem="todoItem"
           v-bind:index="index"
           v-on:remove-todo="removeToDo"
           v-on:save-todo="saveTodo"
        />
       </ul>
    </div>
</template>
<script>
    import todoItem from '@/components/todoItem.vue';
    export default{
        data() {
          return {
            isEdited: false,
          }
        },
        props: ['todos'],
        components: {
            todoItem
        },
        methods: {
            removeToDo(id) {
                this.$emit('remove-todo',id);
            },
            saveTodo(i,retitle) {
                this.$emit('save-todo',i,retitle);
            }
        }
    }
</script>
<style>
    ul{
        list-style: none;
    }
</style>
