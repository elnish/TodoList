<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <p>
            <input type="checkbox" v-on:change="makeComplete">
            {{ todo.title }}
            <button @click="$emit('del-todo', todo.id)" class="del">x</button>
            </p>
    </div>
</template>

<script>
export default {
    name: 'Todoitem',
    props: ["todo"],
    methods: {
        makeComplete() {
            this.todo.completed = !this.todo.completed;
        }
    }
}
</script>

<style scoped>
    .todo-item {
        background: #f4f4f4;
        padding: 10px;
        border-bottom: 1px #ccc dotted;
    }
    .is-complete {
        text-decoration: line-through;
    }
    .del {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
        opacity: .1;
        transition: opacity .7s ease-in-out;
    }
    .del:hover {
        opacity: 1;
    }
</style>


