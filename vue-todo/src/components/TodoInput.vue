<template>
    <div class="inputBox shadow">
      <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
<!--      <button v-on:click="addTodo">add</button>-->
      <span class="addContainer" v-on:click="addTodo">
        <i class="fas fa-plus addBtn"></i>
      </span>
    </div>
</template>

<script>
    export default {
        data: function () {
          return {
            newTodoItem: ""
          }
        },
        methods: {
          addTodo: function () {
            if(this.newTodoItem !== '') {
              var obj = { completed: false, item: this.newTodoItem }
              console.log(this.newTodoItem);
              // 텍스트값만 추가하는게 아니라 텍스트가 추가되었을때 Boolean값 까지 추가
              localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
            }
            this.clearInput();
          },
          clearInput: function () {
            this.newTodoItem = '';
          }
        }
    }
</script>

<style scoped>
  input:focus{
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
  }
  .addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color: white;
    vertical-align: middle;
  }
</style>
