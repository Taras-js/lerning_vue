<template>
  <form @submit.prevent>
    <h2>Создание поста</h2>
<!--    Старый вариант связывания input -->
<!--    <input-->
<!--        v-bind:value="post.titles"-->
<!--        @input="post.titles = $event.target.value"-->
<!--        class="input"-->
<!--        type="text"-->
<!--        placeholder="Название">-->
<!--    <input-->
<!--        v-bind:value="post.body"-->
<!--        @input="post.body = $event.target.value"-->
<!--        class="input"-->
<!--        type="text"-->
<!--        placeholder="Описание">-->
<!--    Новый v-modal-->
        <my-input
            v-model="post.title"
            type="text"
            placeholder="Название"/>
        <my-input
            v-model="post.body"
            type="text"
            placeholder="Описание"/>
    <my-button
               style="align-self: flex-end; margin-top: 15px"
            @click="createPost"
    >Добавить пост</my-button>
  </form>
</template>

<script>
export default {
  name: "PostForm",
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now()
      this.$emit('create', this.post)
      this.post = {
        titles: '',
        body: ''
      }
    }
  },
  watch: {
    post: {
      handler(newValue) {
        console.log(newValue)
      },
      // deep tracking
      deep: true
    }
  }
}
</script>

<style scoped>

form {
  display: flex;
  flex-direction: column;

}
</style>