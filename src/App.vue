<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <input type="text" v-model.trim="modificatorValue">
    <my-button @click="fetchPosts">Получить пост</my-button>
    <my-button
      @click="showDialog"
    >
      Создать пользователя
    </my-button>
    <my-dialog v-model:show="dialogVisible">
      <post-form
        @create="createPost"
      />
    </my-dialog>

    <post-list
      v-bind:posts="posts"
      @remove="removePost"
      />
  </div>
</template>

<script>
  import PostForm from './components/PostForm';
  import PostList from '@/components/PostList';
  import axios from 'axios';
  export default {
    components: {
      PostForm,
      PostList,
    },
    data() {
      return {
        posts: [],
        dialogVisible: false,
        modificatorValue: '',
      }
    },
    methods: {
      createPost(post, second) {
        this.posts.push(post);
        this.dialogVisible = false;
        console.log(second);
      },
      removePost(post) {
        this.posts = this.posts.filter(p => p.id !== post.id);
      },
      showDialog() {
        this.dialogVisible = true;
      },
      async fetchPosts() {
        try {
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
          this.posts = response.data;
          console.log(response.data);
        } catch (e) {
          alert('Ошибка')
        }
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
</style>
