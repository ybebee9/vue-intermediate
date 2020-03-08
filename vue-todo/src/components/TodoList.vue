<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
        <i class="checkBtn fas fa-check" v-bind:class="{ checkBtnCompleted: todoItem.completed }"
           v-on:click="toggleComplete(todoItem,index)" ></i>
<!--        정리할 개념 1 : todoItem.completed 값이 trun이냐 false이냐 에 따라 textCompleted가 활성화 되거나 비활성화 됨.-->
        <span v-bind:class="{ textCompleted: todoItem.completed }">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
    export default {
        props: ['propsdata'],
        methods: {
          removeTodo: function (todoItem, index) {
            this.$emit('removeItem',todoItem,index);
          },
          toggleComplete: function (todoItem, index) {
            // 정리할 개념 2 : = ! 연산자
            // todoItem.completed = ! todoItem.completed 하면 false 인 경우 -> true로, true인 경우 -> false로 변경됨
            // To-do 리스트에서 끝낸줄 알고 체크완료 했는데 미처 덜 끝난일이 있어서 다시 체크해제 할수 있도록 이 연산자 사용해서
            // true, false값 변경시키는 부분임
            todoItem.completed = ! todoItem.completed
            // 로컬 스토리지 데이터를 갱신
            console.log(todoItem.item);
            // 정리할 개념 3 : removeItem을 하면 왜 localStorage에서 삭제되지 않는지 ... 그리고 38번 라인 주석처리해도 결과값은 똑같음..
            localStorage.removeItem(todoItem.item);
            console.log(JSON.stringify(todoItem.item));
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
          }
        }
    }
</script>

<style scoped>
  ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0px;
    text-align: left;
  }
  li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
  }
  .checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-left: 5px;
  }
  .checkBtnCompleted {
    color: #b3adad;
  }
  .textCompleted {
    text-decoration: line-through;
    color: #b3adad;
  }
  .removeBtn {
    margin-left: auto;
    color: #de4343;
  }
</style>
