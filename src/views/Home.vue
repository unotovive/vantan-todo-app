<template>
  <div class="home">
    <h1 class="title">はじめてのTODOアプリ</h1>
    <section class="control">
      <h2 class="section-title">タスクを追加</h2>
      <input
        type="text"
        placeholder="タスクを入力"
        class="input"
        v-model="input"
      />
      <v-button @click="createTodo()">追加</v-button>
    </section>
    <section class="todo-list-group">
      <h2 class="section-title">完了済みタスク</h2>
      <ul class="todo-list">
        <li class="todo-item" v-for="item in completeTodoList" :key="item.id">
          <label for="">
            <input type="checkbox" v-model="item.checked" />
            {{ item.name }}
          </label>
          <v-button @click="deleteTodo(item.id)">削除</v-button>
        </li>
      </ul>
    </section>
    <section class="todo-list-group">
      <h2 class="section-title">未完了タスク</h2>
      <ul class="todo-list">
        <li class="todo-item" v-for="item in inCompleteTodoList" :key="item.id">
          <label for="">
            <input type="checkbox" v-model="item.checked" />
            {{ item.name }}
          </label>
          <v-button @click="deleteTodo(item.id)">削除</v-button>
        </li>
      </ul>
    </section>
    <section class="todo-list-group">
      <h2 class="section-title">全てのタスク</h2>
      <ul class="todo-list">
        <li class="todo-item" v-for="item in todoList" :key="item.id">
          <label for="">
            <input type="checkbox" v-model="item.checked" />
            {{ item.name }}
          </label>
          <v-button @click="deleteTodo(item.id)">削除</v-button>
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
import VButton from "@/components/VButton.vue";

export default {
  name: "Home",
  components: {
    VButton,
  },
  data() {
    return {
      todoList: [
        { name: "牛乳買ってくる", checked: false, id: 1 },
        { name: "髪切る", checked: true, id: 2 },
      ],
      input: "",
    };
  },
  computed: {
    completeTodoList() {
      return this.todoList.filter((item) => item.checked);
    },
    inCompleteTodoList() {
      return this.todoList.filter((item) => !item.checked);
    },
  },
  methods: {
    createTodo() {
      this.todoList.push({
        name: this.input,
        checked: false,
        id: Math.random(),
      });
      this.input = "";
    },
    deleteTodo(id) {
      const delId = this.todoList.findIndex((item) => {
        return item.id === id;
      });
      this.todoList.splice(delId, 1);
    },
  },
};
</script>
<style scoped>
.home {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #fafaff;
  min-height: 100vh;
}
.title {
  font-size: 28px;
  font-weight: bold;
  margin: 2rem;
}
.section-title {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 0.5rem;
}
.control {
  padding: 12px;
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 3px 5px rgba(0, 0, 0, 0.3);
  margin-bottom: 2rem;
  width: 320px;
}
.todo-list-group {
  padding: 12px;
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 3px 5px rgba(0, 0, 0, 0.3);
  margin-bottom: 2rem;
  width: 320px;
}
.todo-item {
  font-size: 18px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}
.input {
  background: #f5f5f5;
  height: 2.4rem;
  margin-right: 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 0 1rem;
  width: 230px;
}
</style>
