<template>
    <div>
        <input type="text" placeholder="할 일을 입력하세요" v-model="newTodo">
        <button @click="addTodo">추가</button>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                newTodo: ""
            }
        },
        methods: {
            addTodo() {
                this.$emit("addTodo", this.newTodo);
                this.newTodo = "";
            }
        }
    }
</script>

<style scoped>

</style>