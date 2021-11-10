<template>
    <div class="post">
      <div><strong>Название:</strong> {{ post.title }}</div>
      <div><strong>Описание:</strong> {{ post.body }}</div>
    </div>
</template>

<script>
  export default {
    props: {
      posts: {
        type: Object,
        required: true,
      }
    }
  }
</script>

<style scoped>

</style>
