<template>
    <div
        v-for="todo in todoList"
        class="todo"
        :class="{'todo--edit': todo.edit}"
        :key="todo.id"
        @click="$emit('editTodo', todo.id)"
    >
        <div class="todo__title">{{ todo.title }}</div>
        <ul>
            <li v-for="todoItem in todo.todo" :key="todoItem.id">
                <label> 
                    <input
                        type="checkbox" 
                        :checked="todoItem.status" 
                        :disabled="!todo.edit"
                    >
                    {{ todoItem.value }}
                </label>
            </li>
        </ul>

        <button class="todo__del" @click.stop="$emit('delTodo', todo.id)"></button>
    </div>
</template>

<script>
export default {
    name: "PrintTodo",

    props: ["todoList"],
    emits: ["editTodo", "delTodo"],

    data() {
        return {

        }
    }
}
</script>

<style lang="scss">
.todo {
    border: 1px solid grey;
    padding: 12px 40px;
    border-radius: 15px;
    cursor: pointer;
    position: relative;
    height: 80px;
    overflow: hidden;

    &:not(:last-child) {
        margin-bottom: 10px;
    }

    &:hover {
        background-color: rgb(240, 240, 240);
    }

    &--edit {
        height: 100%;
    }
    

    &__title {
        font-size: 20px;
        margin-bottom: 15px;
    }

    &__del {
        cursor: pointer;
        position: absolute;
        right: 30px;
        top: 19px;
        transition: all 0.2s;

        &:before, &:after {
            content: "";
            position: absolute;
            width: 17px;
            height: 4px;
            background: gray;
        }

        &:before {
            transform: rotate(45deg);
        }

        &:after {
            transform: rotate(-45deg);
        }

        &:hover {
            transform:scale(1.2);
        }
    }
}
</style>