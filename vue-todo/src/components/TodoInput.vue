<template>
  <div class="inputBox shadow">
      <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
      <!-- <button v-on:click="addTodo">add</button> -->
      <span class="addContainer" v-on:click="addTodo">
          <i class="fas fa-plus addBtn"></i>
      </span>


    <Modal v-if="showModal" @close="showModal = false">
        <h3 slot="header">경고</h3>
        <div slot="body">
            하이루루~
        </div>
        <span slot="footer" @click="showModal = false">
             할 일을 입력하세요.
            <i class="closeModalBtn fa fa-times" aria-hidden="true"></i>
        </span>
    </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
    data() {
        return {
            newTodoItem: "",
            showModal: false
        }
    },
    methods: {
        addTodo(newTodoItem) {
            if (this.newTodoItem !== '') {
                // this.$emit('addTodoItem', this.newTodoItem)
                const text = this.newTodoItem.trim();
                this.$store.commit('addOneItem', text);
                this.clearInput();
            }
            else {
            this.showModal = !this.showModal;
            }
        },
        clearInput() {
            this.newTodoItem = "";
        }
    },
    components: {
        // Modal: Modal
        Modal
    }
}
</script>

<style>
    .inputBox {
        background: white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }
    .inputBox input {
        border-style: none;
        font-size: 0.9rem;
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
