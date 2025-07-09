<template>
  <div id="app">
    <TodoHeader />
    <TodoInput @addTodo="addOneItem" @showModal="handleShowModal" />
    <TodoList
      :todoItems="todoItems"
      @removeItem="removeOneItem"
      @toggleComplete="toggleOneItem"
    />
    <TodoFooter @clearTodo="clearAllItems" />
    <Modal :show="showModal" @close="closeModal">
      <template #header>
        <h3>알림</h3>
      </template>
      <template #body>
        <p>아무것도 입력하지 않았습니다.</p>
      </template>
    </Modal>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";
import Modal from "./components/common/Modal.vue";

export default {
  data() {
    return {
      todoItems: [],
      showModal: false,
    };
  },
  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i)))
          );
        }
      }
    }
  },
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter,
    Modal,
  },
  methods: {
    addOneItem(todoItem) {
      var obj = { completed: false, item: todoItem };
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem(todoItem, index) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    toggleOneItem(todoItem, index) {
      // 방법 1
      // todoItem.completed = !todoItem.completed;
      // 방법 2
      this.todoItems[index].completed = !this.todoItems[index].completed;

      // 로컬 스토리지의 데이터를 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItems() {
      localStorage.clear();
      this.todoItems = [];
    },
    closeModal() {
      this.showModal = false;
    },
    handleShowModal() {
      this.showModal = true;
    },
  },
};
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f6;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
