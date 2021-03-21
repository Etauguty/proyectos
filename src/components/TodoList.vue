<template>
    <div class="containerTodo">
        <h5 style="text-align:left">To Do List</h5>
        <input type="text" class="todo-input" placeholder="Escribe una tarea" v-model="newTodo" @keyup.enter="addTodo()">
        <button type="submit" class="submit-button" @click="addTodo()">Agregar</button>

        <div v-for="(todo,index) in todos" :key="todo.id" class="todo-item">
            <div class="todo-item-left">             
                <div v-if="!todo.editing" class="todo-item-label"><li>{{todo.title}}</li></div>
                <input v-else class="todo-item-edit" type="text" v-model="todo.title" 
                @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" 
                @keyup.esc="cancelEdit(todo)" v-focus>
                <img v-if="(todo.editing == true)" @click="addTodo()" src="../assets/icon-disk.svg">
            </div>
            <div class="items">
                <img @click="editTodo(todo)" src="../assets/icon-pen.svg">
                <img @click="removeTodo(index)" src="../assets/icon-trash.svg">
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TodoList',
    data () {
        return{
            newTodo: '',
            idForTodo: 3,
            beforeEditCache : '',
            todos: [
                {
                    'id':1,
                    'title': 'Task 01',
                    'completed': false,
                    'editing': false,
                },
                {
                    'id':2,
                    'title': 'Task 02',
                    'completed': false,
                    'editing': false,
                }
            ]
        }
    },

    //Permite el autofocus 
    directives: {
        focus: {
            inserted: function (el) {
            el.focus()
            }
        }
    },

    methods:{
        //Método para agregar tareas
        addTodo(){
            //Checa que no se agreguen espacios en blanco
            if(this.newTodo.trim().length == 0){
                return
            }

            this.todos.push({
                id: this.idForTodo,
                title: this.newTodo,
                completed: false,
                editing: false,
            })

            this.newTodo = ''
            this.idForTodo++
        },
        //Método para editar tareas
        editTodo(todo){
            this.beforeEditCache = todo.title
            todo.editing = true;
        },
        //Método para no permitir tareas en blanco
        doneEdit(todo){
            if(todo.title.trim() == ''){
                todo.title = this.beforeEditCache
            }
            todo.editing = false;
        },
        //Método para no editar en caso de presionar escape
        cancelEdit(todo){
            todo.title = this.beforeEditCache;
            todo.editing = false;
        },
        //Método para remover tarea
        removeTodo(index){
            this.todos.splice(index, 1)
        }
    }
}
</script>

<style>
    /*Ajusta al contendedor*/
    *{
        box-sizing: border-box;
    }

    /*Edita el contenedor principal*/
    .containerTodo{
    max-width: 550px;
    max-height: 550px;
    margin: 0 auto;
    background-color:#E7E7E7;
    padding: 5px;
    padding-bottom: 50px;
    }

    /*Edita el área de ingreso de texto*/
    .todo-input{
        width: 81%;
        padding: 10px 10px;
        font-size: 14px;
        margin-bottom: 16px;
    }

    /*Edita el área de tareas*/
    .todo-item{
        margin: auto;
        padding: 10px;
        font-size: 14px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        background-color: lightgrey;
    }
    
    /*Edita el área de tareas al momento de editar*/
    .todo-item-edit{
        font-size: 14px;
        color: #2c3e50;
        margin-left: 12px;
        width: 100%;
        display: inline-block;
        padding: 18px;
        border-color: red;
    }
    
    /*Edita el boton de agregar*/
    .submit-button {
        background: #0066A2;
        color: white;
        border-style: outset;
        border-color: #0066A2;
        height: 40px;
        width: 100px;
        font: bold 15px arial, sans-serif;
        text-shadow:none;
    }

    /*Edita ela rea de los botones para editar y eliminar*/
    .items{
        margin: 5px;
    }
</style>
