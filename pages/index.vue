<!-- pages/index.vue -->
<template>
  <div>
    <section class="container">
      <h1>Todoリスト</h1>
      <div class="addArea">
        <input type="text" name="addName" v-model="content">
        <button class="button button--green" @click="insert">追加</button>
      </div>
      <table class="Lists">
        <thead>
          <tr>
            <th>登録日時</th>
            <th>タスク</th>
            <th>削除</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in todos" :key="index">
            <td>{{ item.created }}</td>
            <td class="Lists-tast">{{ item.content }}</td>
            <td><button class="button button--delete" @click="remove(todos)">削除</button></td>
          </tr>
        </tbody>
      </table>
    </section>
  </div>
</template>
<script>
  import {mapState} from 'vuex';

  export default {
    data: function() {
      return {
        content: ''
      };
    },
    computed: {
      ...mapState(['todos'])
    },
    methods: {
      insert: function() {
        if(this.content != ''){
          this.$store.commit('insert', {content: this.content});
          this.content = '';
        }
      },
      remove: function(todos){
        this.todos.splice(todos, 1);
      }
    }
  };
  
</script>
<style>
body{
  background-color: midnightblue;
  width: 100vw;
  height: 100vh;
}
.container{
  position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  width: 50%;
  margin: auto;
  padding: 20px;
  border-radius: 10px;
  background-color: white;
}
.addArea{
  text-align: center;
  margin: 30px;
}
.addArea input{
  height: 30px;
  width: 80%;
}
.addArea button{
  padding: 8px;
  border-radius: 5px;
  background-color: white;
  border: solid 2px purple;
  color: purple;
}
.addArea button:hover{
  background-color: purple;
  border: solid 2px white;
  color: white;
}
.Lists{
  text-align: center;
  width: 90%;
  margin: 30px;border-collapse: separate;
  border-spacing: 0px 8px;  
}
.button--delete{
  padding: 8px;
    border-radius: 5px;
    background-color: white;
    border: solid 2px turquoise;
    color: turquoise;
}
.button--delete:hover{
  background-color: turquoise;
    border: solid 2px turquoise;
    color: white;
}
</style>