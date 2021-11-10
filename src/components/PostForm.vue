<template>
    <form @submit.prevent>
      <h4>Создание поста</h4>
      <my-input v-model="post.title" class="input" type="text" placeholder="Название"/>
      <my-input v-model="post.body" class="input" type="text" placeholder="Описание"/>
      <my-button
        class="btn"
        @click="createPost"
      >
        Создать
      </my-button>
    </form>
</template>

<script>
  export default {
    data() {
      return {
        post: {
          title: '',
          body: '',
        }
      }
    },
    methods: {
      createPost() {
        this.post.id = Date.now();
        this.$emit('create', this.post, 'second param');
        this.post = {
          title: '',
          body: '',
        }
      },
    }
  }
</script>

<style scoped>
  form {
    display: flex;
    flex-direction: column;
  }

  button {
    margin-top: 15px;
    align-self:flex-end;
  }
</style>
