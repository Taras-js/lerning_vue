<template>
  <div v-if="posts.length > 0">
    <h3>Список пользователей</h3>
    <transition-group name="post-list">
      <post-item
          :post="post"
          v-for="post in posts"
          :key="post.id"
          @remove="$emit('remove', post)"
      />
    </transition-group>

  </div>
  <h2 v-else style="color: red">
    Список постов опустел
  </h2>
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
.post-list {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.5s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
</style>