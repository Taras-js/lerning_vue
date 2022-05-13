<template>

    <div class="post">
      <div>
        <div><strong>Название:</strong> {{ post.titles }}</div>
        <div><strong>Описание:</strong> {{ post.body }}</div>
      </div>
      <div class="post__btns">
        <my-button>Удалить пост</my-button>
      </div>
    </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
export default {
  name: "PostItem",
  components: {MyButton},
  props: {
    post: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.post {
  padding: 20px;
  border: 2px solid orangered;
  margin-top: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>