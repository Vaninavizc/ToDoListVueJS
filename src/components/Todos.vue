<template>
    <section class="todoapp">
        <header class="header">
            <h1>Todo</h1>
            <input type="texte" class="new-todo" placeholder="Ajouter une tache" v-model="newTodo" @keyup.enter="addTodo">

        </header>
        <div class="main">
            <ul class="todo-list">
                <li class="todo" v-for="todo in filteredTodos" :class="{completed: todo.completed}">
                    <div class="view">
                        <input type="checkbox" v-model="todo.completed" class="toggle">
                        <label>{{ todo.name }}</label>
                    </div>
                </li>
            </ul>
        </div>
        <footer>
            <span class="todo-count"><strong>{{ remaining}}</strong> Tâches à faire</span> <br>
            <ul class="filters">
                <li>
                    <a href="#" :class="{selected : filter === 'all'}" @click.prevent="filter = 'all'">Toutes</a>
                </li>
                <li>
                    <a href="#":class="{selected : filter === 'todo'}" @click.prevent="filter = 'todo'">A faire</a>
                </li>
                <li>
                    <a href="#" :class="{selected : filter === 'done'}" @click.prevent="filter = 'done'">Faites</a>
                </li>
            </ul>
        </footer>
    </section>
</template>

<script>
    export default{
        data(){
            return{
                todos:[{
                    name: 'Tache de test',
                    completed: false
                }],
                newTodo:'',
                filter:'all'
            }
        },
        methods:{
            addTodo(){
                this.todos.push({
                    completed:false,
                    name: this.newTodo
                })
                this.newTodo=''
            }
        },
        computed:{
            remaining(){
                return this.todos.filter(todo => !todo.completed).length
            },
            filteredTodo(){
                if(this.filter === 'todo'){
                    return this.todos(todo => !todo.completed)
                } else if (this.filter === 'done'){
                    return this.todos(todo => todo.completed)
                }
                return this.todos
            }
        }
    }
</script>

<style src="./todo.css"></style>