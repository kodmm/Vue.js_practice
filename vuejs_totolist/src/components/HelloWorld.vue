<template>
  <div class="container">
    {{ msg }}
    <div class="left-containter">
      <form>
        <button @click="addTodo()">ADD TASK</button>
        <button @click="removeTodo()">DELETE FINISHED TASKS</button>
        <p>input: <input type="text" v-model="newTodo"></p>
        <p>task: {{ newTodo }}</p>
      </form>
      <div class="task-list">
      <label class="task-list_item"
              v-for="todo in todos"
              v-bind:class="{ 'task-list_item--checked': todo.done}"
      >
              <input type="checkbox" v-model="todo.done">
              <input type="checkbox" v-model="todo.editing">
              <input v-if="todo.editing" v-model="todo.text" @keyup.enter="todo.editing = !todo.editing">
              <span v-else>{{ todo.text }}</span>
        </label>
        
      </div>
    </div>
    <div class="center-container">
        <Timeline
           id="twitterdev"
           sourceType="profile"
           :options="{tweetLimit: '3'}"
        />
    </div>
    <div class="right-container">
        <Timeline
           id="webcamp_io"
           sourceType="profile"
           :options="{tweetLimit: '3'}"
        />
    </div>
  </div>
</template>

<script>
import { Timeline } from 'vue-tweet-embed';
  export default {
    components: {
      Timeline
    },
    name: 'hello',
    data () {
      return {
        msg: 'welcome to your vue.js App',
        todos: [
          {text: 'vue-router', done: false, editing: false},
          {text: 'vuex', done: false, editing: false},
          {text: 'vue-loader', done: false, editing: false},
          {text: 'awesome-vue', done: true, editing: false},
        ],
        newTodo: ""
      }
    },
    methods: {
      addTodo: function(event) {
        let text = this.newTodo.trim()
        if (!text) {
          return
        }
        this.todos.push({
          text: text,
          done: false,
          editing: false,
        })
        this.newTodo = ''
      },
      removeTodo: function(event) {
        for (let i = this.todos.length -1; i >= 0; i--) {
          if (this.todos[i].done) this.todos.splice(i, 1)
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
@mixin flex-vender() {
  display: flex;
  display: -webkit-flex;
  display: -moz-flex;
  display: -ms-flex;
  display: -o-flex;
}
.container {
  display: flex;
   flex-flow: row wrap;
}
.task-list {
  @include flex-vender;
  flex-direction: column;
  align-items: center;

  &_item {
    width: 270px;
    text-align: left;
    $element: #{&};
    &--checked {
      @extend #{$element};
      color: #85a6c6;
    }
  }
}
.TwitterContainer {
  @include flex-vender;
  flex-direction: column;
  align-items: right;
}
</style>
