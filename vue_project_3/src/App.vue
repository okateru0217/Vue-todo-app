<template>
  <div>
    <h1>ToDoリスト</h1>

    <input 
    type="radio" 
    id="all" 
    value="すべて" 
    v-model="chengeoverTask">
    <label for="all">すべて</label>
    
    <input 
    type="radio" 
    id="working" 
    value="作業中" 
    v-model="chengeoverTask">
    <label for="working">作業中</label>
    
    <input 
    type="radio" 
    id="done" 
    value="完了" 
    v-model="chengeoverTask">
    <label for="done">完了</label>

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
        v-for="(todo, index) in todos" 
        :key="index">
          <td>{{ todo.id }}</td>
          <td>{{ todo.comment }}</td>
          <td><button>{{ todo.status }}</button></td>
          <td><button>{{ todo.delete }}</button></td>
        </tr>
      </tbody>
    </table>

    <h2>新規タスクの追加</h2>
    <input type="text" v-model="task">
    <button @click="addTaskBtn">追加</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      task: '',
      chengeoverTask: 'すべて'
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
        delete: '削除'
      });
      this.task = '';
    }
  }
}
</script>