<script>
export default {
    data() {
        return {
            todo: '',
            todos: [],
            todosCompleted: []
        }
    },
    methods: {
        submitTodo($event) {
            $event.preventDefault();
            this.todos.push(this.todo)
            this.todo = ''
            console.log(this.todos)
        },
        removeTodo(index) {
            this.todos.splice(index, 1)
        },
        finishTodo(todoP, index) {
            console.log(this.todos[index])
            this.todosCompleted.push(this.todos[index])
            this.todos = this.todos.filter(todo => { return todo !== todoP })
        }
    }
}
</script>
<template>
    <div class="container">
        <form class="form-container">
            <input type="text" class="inputTxt" v-model="todo" placeholder="Digite a tarefa a ser realizada">
            &nbsp;
            <div class="buttons-container">
                <button @click="cancelTodo()">Cancelar</button>
                &nbsp;
                <button @click="submitTodo($event)">Salvar</button>
            </div>
        </form>

        <br>
        <h2>A Fazer</h2>
        <table v-show="todos.length > 0" class="table-container">
            <thead>
                <tr class="table-h-item">
                    <td><b>Ordem</b></td>
                    <td><b>Descrição</b></td>
                </tr>
            </thead>
            <tbody v-for="(todo, index) in todos">
                <tr class="table-b-item">
                    <td>{{ index }}</td>
                    <td>{{ todo }}</td>
                    <button @click="removeTodo(index)">Remover</button>
                    &nbsp;
                    <button @click="finishTodo(todo, index)">Feito</button>
                </tr>
            </tbody>
        </table>
        <hr>
        <h2>Feito</h2>
        <table v-show="todosCompleted.length > 0" class="table-container">
            <thead>
                <tr class="table-h-item">
                    <td><b>Ordem</b></td>
                    <td><b>Descrição</b></td>
                </tr>
            </thead>
            <tbody v-for="(todo, index) in todosCompleted">
                <tr class="table-b-item">
                    <td>{{ index }}</td>
                    <td>{{ todo }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<style scoped>

button {
    border-radius: 10px;
    padding: 10px;
}

.container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    /* height: 100%;
    width: 100%; */
    font-family: Arial, Helvetica, sans-serif;
}

.form-container {
    border: #000000 solid 2px;
    border-radius: 5px;
    width: 450px;
    height: 200px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    place-items: center;
    background-color: #222222;
    box-shadow: 0px 0px 80px 3px #000000;
    transition: box-shadow 2s ease;
}

.form-container:hover {
    border: #000 solid 0.5px;
    box-shadow: 0px 0px 28px 12px #000000;
}

.inputTxt {
    padding: 30px;
    height: 5px;
    width: 75%;
    text-align: center;
}

.table-container {
    border: 5px solid #000;
    text-align: center;
}

.table-h-item td {
    padding: 0 5px 0 0;
}

.table-b-item {
    border: 5px solid #000;
}

.table-b-item td {
    padding: 0 5px 0 0;
}
</style>
