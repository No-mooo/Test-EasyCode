<template>
    <div class="startPage">
        <div class="container">
            <TodoList />
        </div>
    </div>
</template>
<script>
import TodoList from '@/components/TodoList.vue'
export default {
    components: { TodoList },
    name: 'Start',

    data() {
        return {

        }
    },
}
</script>
<style lang="scss">

</style>