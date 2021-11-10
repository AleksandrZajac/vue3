<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <input type="text" v-model.trim="modificatorValue">
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
      v-if="!isPostLoading"
      />
      <div v-else>Идет загрузка...</div>
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
        isPostLoading: false,
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
          this.isPostLoading = true;
          setTimeout(async() => {
           	const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
            this.posts = response.data;
            this.isPostLoading = false;
          }, 1000);
        } catch (e) {
          alert('Ошибка')
        } finally {
        }
      }
    },
    mounted() {
      this.fetchPosts();
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
