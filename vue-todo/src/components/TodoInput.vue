<template>
  <div class="inputBox shadow">
    <input
      type="text"
      placeholder="할 일을 입력하세요"
      v-model="newTodo"
      @keyup.enter="addTodo"
    />
    <!-- <button @click="addTodo">추가</button> -->
    <span class="addContainer" @click="addTodo">
      <i class="fa-solid fa-plus addBtn"></i>
    </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: "",
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo !== "") {
        this.$emit("addTodo", this.newTodo);
        this.clearInput();
      } else {
        this.$emit("showModal");
      }
    },
    clearInput() {
      this.newTodo = "";
    },
  },
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
  margin-left: 10px;
  width: 80%;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
</style>
