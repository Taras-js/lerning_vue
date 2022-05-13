<template>
  <div>
    <h3>Список пользователей</h3>
      <post-item
          :post="post"
          v-for="post in posts"/>

  </div>
<!--  Перенесли в PostItem-->
<!--  <div class="post" v-for="post in posts">-->
<!--    <div><strong>Название:</strong> {{ post.titles }}</div>-->
<!--    <div><strong>Описание:</strong> {{ post.body }}</div>-->
<!--  </div>-->
</template>

<script>
import PostItem from "@/components/PostItem";
export default {
  name: "PostList",
  components: {PostItem},
  props: {
    posts: {
      type: Array,
      required: true,

    }
  }
}
</script>

<style scoped>

</style>