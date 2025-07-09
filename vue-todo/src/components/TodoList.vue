<template>
  <div>
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem, index) in todoItems" :key="index" class="shadow">
        <i
          class="checkBtn fa-solid fa-check"
          :class="{ checkBtnCompleted: todoItem.completed }"
          @click="toggleComplete(todoItem, index)"
        ></i>
        <span :class="{ textCompleted: todoItem.completed }">{{
          todoItem.item
        }}</span>
        <span class="removeBtn" @click="removeTodo(todoItem, index)">
          <i class="fa-solid fa-trash-can"></i>
        </span>
      </li>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: {
    todoItems: {
      type: Array,
      required: true,
    },
  },
  methods: {
    removeTodo(todoItem, index) {
      this.$emit("removeItem", todoItem, index);
    },
    toggleComplete(todoItem, index) {
      this.$emit("toggleComplete", todoItem, index);
    },
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  border-radius: 5px;
  background: white;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5rem;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

/* 리스트 아이템 트랜지션 효과 */
.list-enter-active,
.list-leave-active {
  transition: all 1s;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
