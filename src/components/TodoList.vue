<template>
    <div class="todoList">
        <div class="todoList__head">
            <h1>Todo List</h1>
            <button class="todoList__add" @click="openModal = true">+</button>
        </div>
        <div>
            <PrintTodo 
                :todoList="todoList"
                @editTodo="editTodo"
                @delTodo="delTodo"
            />
        </div>
    </div>

    <ModalCreateTodo
        v-if="openModal"
        @closeModal="openModal = false"
        @sendingTodo="addTodo"
    />
</template>
<script>
import { toRaw } from 'vue';
import ModalCreateTodo from './ModalCreateTodo.vue';
import PrintTodo from './PrintTodo.vue';

export default {
    name: "TodoList",

    components: {
        ModalCreateTodo,
        PrintTodo,
    },

    data() {
        return {
            openModal: false,
            todoList: [
                {
                    id: 1,
                    edit: false,
                    title: 'Список дел на сегодня',
                    todo: [
                        {
                            id: 1,
                            value: 'Создать план на сегодня',
                            status: false,
                        },

                        {
                            id: 2,
                            value: 'Выполнить 1-й пункт',
                            status: false,
                        },

                        {
                            id: 3,
                            value: 'Осознать, что 2-е вещи уже сделаны',
                            status: false,
                        },

                        {
                            id: 4,
                            value: 'Отдохнуть от проделанной работы',
                            status: false,
                        },
                    ],
                },

                {
                    id: 2,
                    edit: false,
                    title: 'sdfsdhdh',
                    todo: [
                        {
                            id: 1,
                            value: 'ertgfgdfdf',
                            status: false,
                        },

                        {
                            id: 2,
                            value: 'ertgfgdfdf',
                            status: false,
                        },

                        {
                            id: 3,
                            value: 'ertgfgdfdf',
                            status: false,
                        },

                        {
                            id: 4,
                            value: 'ertgfgdfdf',
                            status: false,
                        },
                    ],
                },

                {
                    id: 3,
                    edit: false,
                    title: 'TTTTTTT',
                    todo: [
                        {
                            id: 1,
                            value: 'TTTTTTT',
                            status: false,
                        },
                    ],
                },

                {
                    id: 4,
                    edit: false,
                    title: 'TTTTTTT',
                    todo: [
                        {
                            id: 1,
                            value: 'TTTTTTT',
                            status: false,
                        },

                        {
                            id: 2,
                            value: 'TTTTTTT',
                            status: false,
                        },

                        {
                            id: 3,
                            value: 'TTTTTTT',
                            status: false,
                        },
                    ],
                },

                {
                    id: 5,
                    edit: false,
                    title: 'TTTTTTT',
                    todo: [
                        {
                            id: 1,
                            value: 'TTTTTTT',
                            status: false,
                        },
                    ],
                },

                {
                    id: 6,
                    edit: false,
                    title: 'TTTTTTT',
                    todo: [
                        {
                            id: 1,
                            value: 'TTTTTTT',
                            status: false,
                        },
                    ],
                },

                {
                    id: 7,
                    edit: false,
                    title: 'TTTTTTT',
                    todo: [
                        {
                            id: 1,
                            value: 'TTTTTTT',
                            status: false,
                        },
                    ],
                },

                {
                    id: 8,
                    edit: false,
                    title: 'TTTTTTT',
                    todo: [
                        {
                            id: 1,
                            value: 'TTTTTTT',
                            status: false,
                        },
                    ],
                },

                {
                    id: 9,
                    edit: false,
                    title: 'TTTTTTT',
                    todo: [
                        {
                            id: 1,
                            value: 'TTTTTTT',
                            status: false,
                        },
                    ],
                },

                {
                    id: 10,
                    edit: false,
                    title: 'TTTTTTT',
                    todo: [
                        {
                            id: 1,
                            value: 'TTTTTTT',
                            status: false,
                        },
                    ],
                },

                {
                    id: 11,
                    edit: false,
                    title: 'TTTTTTT',
                    todo: [
                        {
                            id: 1,
                            value: 'Fooooo',
                            status: false,
                        },
                    ],
                },


            ],
        }
    },

    methods: {
        editTodo(id) {
            const targetTodo = this.todoList[this.todoList.findIndex(item => item.id == id)];

            if (targetTodo == -1 || targetTodo?.edit) return;

            const searchOpenTodo = this.todoList.findIndex(item => item.edit);
            if (searchOpenTodo != -1) this.todoList[searchOpenTodo].edit = false;

            targetTodo.edit = true;
        },

        delTodo(id) {
            if (!confirm("Delete a note ?")) return;

            const searchTodo = this.todoList.findIndex(item => item.id == id);
            this.todoList.splice(searchTodo, 1);
        },

        addTodo(todo) {
            this.todoList.push(
                {
                    id: toRaw(this.todoList.at(-1)).id + 1,
                    edit: false,
                    title: todo.title,
                    todo: todo.listTodo.map(item => {
                        return {
                            ...item,
                            status: false
                        }
                    })
                },
            )
        }
    }
}
</script>
<style lang="scss">
.todoList {
    margin-bottom: 15px;

    &__head {
        padding-top: 30px;
        margin-bottom: 50px;
        display: flex;
        justify-content: space-around;
        align-items: flex-end;
        position: sticky;
        top: 0;
        padding-bottom: 10px;
        background: white;
        z-index: 1;

        & h1 {
            font-size: 24px;
        }

        &::after {
            content: '';
            display: block;
            width: 60%;
            position: absolute;
            height: 1px;
            background-color: black;
            bottom: 0;
        }
    }

    &__add {
        font-size: 25px;
        border: 1px solid grey;
        padding: 3px 10px;
        border-radius: 55px;
    }
}
</style>