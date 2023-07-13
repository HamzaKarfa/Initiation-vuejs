<script>



export default {
    name: "TodoDetails",
    setup(props) {
        console.log(props)
    },
    props: ["selectedTodo"],
    data() {
        return {
            isEditable: false,
            todo: this.selectedTodo,
        }
    },
    methods: {
        updateTodo() {
            this.$emit("updateTodo", this.todo);
            this.isEditable = false;
        },
    },

};
</script>

<template>
    {{ console.log(this.props) }}
    <div v-if="todo">
        <h2>Details</h2>
        <button @click="isEditable = !isEditable">Edit</button>
        <div v-if="isEditable">
            <input type="text" v-model="todo.name" />
            <input type="text" v-model="todo.description" />
        </div>
        <div v-else>
            <h4>{{ todo.name }}</h4>
            <p>{{ todo.description }}</p>
        </div>
        <p>{{ todo.done ? 'Done' : 'To Do' }}</p>
    </div>
</template>
