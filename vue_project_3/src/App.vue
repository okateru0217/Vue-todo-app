<template>
  <div class="container">
    <div class="title">
      <h1>ToDoリスト</h1>
    </div><!-- title -->
    <div class="task_status">
      <input 
      type="radio" 
      id="all" 
      value="すべて" 
      v-model="taskStatus">
      <label for="all">すべて</label>
      <input 
      type="radio" 
      id="working" 
      value="作業中" 
      v-model="taskStatus">
      <label for="working">作業中</label>
      <input 
      type="radio" 
      id="done" 
      value="完了" 
      v-model="taskStatus">
      <label for="done">完了</label>
    </div><!-- task_status -->
    <div class="task_table">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>コメント</th>
            <th>状態</th>
          </tr>
        </thead>
        <tbody>
          <tr 
          v-for="(todo, index) in filterTask" 
          :key="index">
            <td>{{ todo.id }}</td>
            <td>{{ todo.comment }}</td>
            <td><button @click="actionStatus(todo)">{{ todo.status }}</button></td>
            <td><button @click="deleteTask(todo)">削除</button></td>
          </tr>
        </tbody>
      </table>
    </div><!-- task_table -->
    <div class="add_task">
      <h2>新規タスクの追加</h2>
      <input type="text" v-model="task">
      <button @click="addTaskBtn">追加</button>
    </div><!-- add_task -->
  </div><!-- container -->
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      task: '',
      taskStatus: 'すべて'
    }
  },
  methods: {
    // 追加ボタン押下時の処理
    addTaskBtn() {
      if (this.task === '') {
        alert('タスクを入力して下さい！');
        return;
      }
      this.todos.push({
        id: this.todos.length,
        comment: this.task,
        status: '作業中',
      });
      this.task = '';
    },
    // 削除ボタン押下時の処理
    deleteTask(todo) {
      const targetIndex = this.todos.indexOf(todo);
      this.todos.splice(targetIndex, 1);
      for (let i = targetIndex; i < this.todos.length; i++) {
        this.todos[i].id = i;
      }
    },
    // statusの切り替え
    actionStatus(todo) {
      if (todo.status === '作業中') {
        todo.status = '完了';
      } else if (todo.status === '完了') {
        todo.status = '作業中';
      }
    }
  },
  computed: {
    // statusの値によって、タスクを切り替え
    filterTask() {
      if (this.taskStatus === 'すべて') {
        return this.todos;
      } else if (this.taskStatus === '作業中') {
        return this.todos.filter((item) => {
          return item.status === '作業中';
        })
      } else if (this.taskStatus === '完了') {
        return this.todos.filter((item) => {
          return item.status === '完了';
        }, this)
      }
      return ''
    }
  }
}
</script>