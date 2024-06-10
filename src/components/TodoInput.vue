<template>
  <div class="inputBox">
    <input
      type="text"
      v-model="newTodoItem"
      placeholder="Type what you have to do"
      v-on:keyup.enter="addTodo"
    />
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>

    <ModalComponent v-if="showModal" @click="showModal = false">
      <template v-slot:header>
        <h3>경고</h3>
      </template>
      <template v-slot:footer>
        <span @click="showModal = false">
          할 일을 입력하세요.
          <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
        </span>
      </template>
    </ModalComponent>
  </div>
</template>

<script>
import ModalComponent from "./common/ModalComponent.vue";

export default {
  components: {
    ModalComponent,
  },
  data() {
    return {
      newTodoItem: "",
      showModal: false,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== "") {
        var value = this.newTodoItem && this.newTodoItem.trim();
        this.$emit("addTodo", value);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = "";
    },
  },
};
</script>

<style>
input:focus {
  outline: none;
}
.inputBox {
  background-color: #fff;
  height: 45px;
  line-height: 45px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
  text-align: left;
}
.addContainer {
  float: right;
  width: 3rem;
  background-color: rgb(202, 168, 168);
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: #fff;
  vertical-align: middle;
}
.closeModalBtn {
  color: #5f0000;
}
</style>