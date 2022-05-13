<template>
<!--  <div class="first">-->
<!--    <h1>This is an first page</h1>-->
<!--  </div>-->
<!--  <div>-->
<!--    <h1>Оцените меня на Vue</h1>-->
<!--    <div>-->
<!--      Старая запись обработчиков событий-->
<!--      <button v-on:click="addLike">Like</button>-->
<!--      <button v-on:click="addDisLike">Dislike</button>-->
<!--Новая запись обработчиков событий-->
<!--      <button @click="addLike">Like</button>-->
<!--      <button @click="addDisLike">Dislike</button>-->

<!--    </div>-->
<!--    <div>Количество лайков: <strong>{{ likes }}</strong></div>-->
<!--    <div>Количество дизлайков: <strong>{{ dislikes }}</strong></div>-->
<!--  </div>-->
<!--  <div>-->
<!--    <div class="post">-->
<!--      <div>-->
<!--        <div><strong>Название:</strong> Пост о Vue</div>-->
<!--        <div><strong>Описание:</strong> Vue мне прямо зашел, я очень этому рад</div>-->
<!--      </div>-->
<!--    </div>-->
<!--  </div>-->
    <div class="first">
      <post-form
          @create="createPost"
      />
<!--      Старая запись-->
<!--      <post-list v-bind:posts="posts" />-->
      <post-list
          :posts="posts"
      />
    </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
export default {
  name: "FirstView",
  components: {
    PostList, PostForm
  },
  // data() {
  //   return {
  //     likes: 0,
  //     dislikes: 10,
  //   }
  // },
  data() {
    return {
     posts: [
       {id: 1, titles: 'Vue', body: 'Vue super'},
       {id: 2, titles: 'React', body: 'React super'},
       {id: 3, titles: 'Express', body: 'Express super'}

     ],
      // Перенесли в PostForm
      // titles: '',
      // body: ''
    }
  },
  methods: {
  //   addLike() {
  //     this.likes += 1
  //   },
  //   addDisLike() {
  //     this.dislikes += 1
  //   }
    createPost(post) {
      this.posts.push(post)

      // console.log(post)
      // console.log(second)
      // console.log(third)

      // Перенесли логику в PostForm
      // const newPost = {
      //   id: Date.now(),
      //   titles: this.titles,
      //   body: this.body
      // }
      // this.posts.push(newPost)
      // this.titles = ''
      // this.body = ''
    },
    // inputBody(event) {
    //   this.body = event.target.value
    // }
  }
}
</script>

<style scoped>
    *{
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    .first {
      padding: 10px;
    }



</style>