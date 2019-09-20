<template>
    <li>
        <span v-bind:class="{completed: todoItem.completed}">
           <input type="checkbox"
              v-on:change="todoItem.completed = !todoItem.completed"
           >
            <span>{{index+1}} {{todoItem.title}}</span>
            <transition
              name="custom-classes-transition"
              enter-active-class="animated tada"
              leave-active-class="animated bounceOutRight"
            >
              <div v-if="isEdited" class="edit-block">
                <input type="text" v-model="retitle" v-bind:placeholder="todoItem.title">
                <button v-on:click="$emit('save-todo',index,retitle)">save</button>
              </div>
            </transition>
        </span>
        <div>
          <button v-on:click="$emit('remove-todo',todoItem.id)">&times;</button>
        </div>
    </li>
</template>
<script>
    export default {
        data() {
          return {
            retitle: '',

          }
        },
        props: {
            todoItem: {
                type: Object,
                required: true
            },
            index: Number,
            isEdited: Boolean,
        },
        computed: {
          b(){
            console.log(this.isEdited)
          }
        }
    }
</script>
<style scoped>
    li{
        border: 1px solid lightgrey;
        border-radius: 5px;
        margin-top: 10px;
        display: -webkit-flex;
        display: -moz-flex;
        display: -ms-flex;
        display: -o-flex;
        display: flex;
        justify-content: space-between;
        padding: 8px;
    }
    input[type="checkbox"]{
        margin-right: 10px;
    }
    button{
        background: #FC3737;
        font-size: 20px;
        color: white;
        cursor: pointer;
        border: 0;
        transition: all ease 0.3s;
    }
    button:hover{
      background: grey;
    }
    .completed{
        text-decoration: line-through;
    }
    .edit-block{

    }
</style>
