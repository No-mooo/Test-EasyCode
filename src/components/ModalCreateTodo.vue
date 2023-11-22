<template>
    <Teleport to="body" >
        <div class="modal" @click="closeModal">
            <form class="modal__content" @submit.prevent="sendingTodo">
                <input v-model="titleTodo" required type="text" placeholder="Title" class="modal__titleTodo">
                
                <p class="modal__todoList">Todo List:</p>
                <ul>
                    <li
                        v-for="todo in listTodo"
                        :key="todo.id"
                    >
                        <input v-model="todo.value" required type="text" placeholder="Todo">
                    </li>
                </ul>

                <button class="modal__addTodo" @click="addTodo">
                    +
                </button>

                <button type="submid" class="modal__create">Create</button>
            </form>
        </div>
    </Teleport>
</template>
<script>
import { toRaw } from 'vue';

export default {
    name: "ModalCreateTodo",
    emits: ["closeModal", "sendingTodo"],

    components: {},

    data() {
        return {
            titleTodo: '',
            listTodo: [
                {
                    id: 1,
                    value: ''
                }    
            ]
        }
    },

    methods: {
        sendingTodo(event) {
            this.$emit("sendingTodo", {
                title: this.titleTodo,
                listTodo: toRaw(this.listTodo)
            });

            this.titleTodo = '';
            this.listTodo[0].value = '';
            this.listTodo.splice(1);
        },

        closeModal(event) {
            if (!event.target.closest(".modal__content")) this.$emit("closeModal");
        },

        addTodo() {
            this.listTodo.push(
                {
                    id: toRaw(this.listTodo.at(-1)).id + 1,
                    value: ''
                }
            )
        }
    }
}
</script>
<style lang="scss">
    .modal {
        font-size: 20px;
        top: 0;
        position: fixed;
        height: 100vh;
        width: 100%;
        background-color: rgba(70, 70, 69, 0.9);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 2;

        &__content {
            padding: 30px;
            border-radius: 10px;
            background-color: rgb(226, 226, 226);
            display: flex;
            flex-direction: column;
        }

        &__titleTodo {
            margin-bottom: 30px;
        }

        &__todoList {
            text-align: center;
            margin-bottom: 15px;
        }

        &__addTodo {
            align-self: center;
            width: 30px;
            margin-top: 20px;
            margin-bottom: 40px;
            color: rgb(24, 70, 197);
            font-weight: 900;
            cursor: pointer;
        }

        &__create {
            background-color: #799fb9;
            width: max-content;
            align-self: center;
            padding: 10px 20px;
            border-radius: 10px;
        }
   
        input {
            border-radius:15px;
            border:0;
            box-shadow:4px 4px 10px rgba(0,0,0,0.06);
            padding: 10px 20px;
        }
    }
</style>