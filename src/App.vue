<template>
  <div class="app">
    <form @submit.prevent>
      <h4>Создание поста</h4>
      <input v-bind:value="title" @input="inputTitle" class="input" type="text" placeholder="Название">
      <input v-bind:value="body" @input="body = $event.target.value" class="input" type="text" placeholder="Описание">
      <button @click="createPost">Создать</button>
    </form>
    <div class="post" v-for="post in posts">
      <div><strong>Название:</strong> {{ post.title }}</div>
      <div><strong>Описание:</strong> {{ post.body }}</div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        posts: [
          {id: 1, title: 'Javascript', body: 'Описание поста'},
          {id: 1, title: 'Javascript 2', body: 'Описание поста 2'},
          {id: 1, title: 'Javascript 3', body: 'Описание поста 3'},
        ],
        title: '',
        body: '',
      }
    },
    methods: {
      createPost() {
        const newPost = {
          id: Date.now(),
          title: this.title,
          body: this.body,
        }
        this.posts.push(newPost);
        this.title = '';
        this.body = '';
      },
    inputTitle(event) {
      this.title = event.target.value;
      }
    }
  }
</script>

<style>
  .app {
    padding: 20px;
  }

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .post {
    padding: 15px;
    border: 1px solid teal;
    margin-top: 15px;
  }

  form {
    display: flex;
    flex-direction: column;
  }

  .input {
    width: 100%;
    border: 1px solid teal;
    padding: 10px 15px;
    margin-top: 15px;
  }
</style>
