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
        <input
            v-model="post.titles"
            class="input"
            type="text"
            placeholder="Название">
        <input
            v-model="post.body"
            class="input"
            type="text"
            placeholder="Описание">
    <my-button
               style="align-self: flex-end; margin-top: 15px"
            @click="createPost"
    >Добавить пост</my-button>
  </form>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
export default {
  name: "PostForm",
  components: {MyButton},
  data() {
    return {
      post: {
        titles: '',
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
  }
}
</script>

<style scoped>
.input {

  border: 2px solid orangered;
  padding: 10px 15px;
  margin-top: 15px;
}
form {
  display: flex;
  flex-direction: column;

}
</style>