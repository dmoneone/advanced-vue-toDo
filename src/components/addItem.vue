<template>
    <form @click.prevent="addItem">
        <input type="text" v-model="title">
        <button type="submit">add</button>
    </form>
</template>


<script>
    export default {
        data() {
            return {
                title: ''
            }
        },
        methods: {
            addItem() {
                if (this.title.trim()) {
                    const newItem = {
                        title: this.title,
                        id: Date.now(),
                        completed: false
                    }
                    this.$emit('add-item',newItem);
                    this.title = '';
                }
            }
        }
    }
</script>


<style scoped>
    form{
        display: -webkit-flex;
        display: -moz-flex;
        display: -ms-flex;
        display: -o-flex;
        display: flex;
        justify-content: space-around;
    }
    input[type="text"]{
        max-width: 2000px;
        box-sizing: border-box;
        padding: 10px;
        width: 100%;
    }
</style>
