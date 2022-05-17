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
      <h1>Страница с постами</h1>
      <my-input
        v-model="searchQuery"
        placeholder="search..."
      >

      </my-input>
      <div class="app__buttons">
        <my-button
            @click="showDialog"

        >
          Создать пост
        </my-button>
        <my-select
          v-model="selectedSort"
          :options="sortOptions"
        />


      </div>
<!--      Убрали кнопку получения постов-->
<!--      <my-button @click="fetchPosts">Fetch posts</my-button>-->

      <my-dialog v-model:show="myDialogVisible">
        <post-form
            @create="createPost"
        />
      </my-dialog>
      <div class="page__wrapper">
        <div v-for="pageNumber in totalPages"
             :key="pageNumber"
             class="page"
             :class="{
               'current-page': page === pageNumber
             }"
             :style="{
                // inline style
             }"
             @click="changePage(pageNumber)"
        >
          {{ pageNumber }}
        </div>
      </div>
<!--      Старая запись-->
<!--      <post-list v-bind:posts="posts" />-->
      <post-list
          :posts="sortedAndSearchesPosts"
          @remove="removePost"
          v-if="!isPostsLoading"
      />
      <div v-else>Loading in progress ...</div>

    </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from  "axios";
import MyInput from "@/components/UI/MyInput";
export default {
  name: "FirstView",
  components: {
    MyInput,
    PostList,
    PostForm
  },
  // data() {
  //   return {
  //     likes: 0,
  //     dislikes: 10,
  //   }
  // },
  data() {
    return {
      posts: [],

      // Моковые данные убрали
     // posts: [
     //   {id: 1, titles: 'Vue', body: 'Vue super'},
     //   {id: 2, titles: 'React', body: 'React super'},
     //   {id: 3, titles: 'Express', body: 'Express super'}
     //
     // ],
      myDialogVisible: false,
      // Перенесли в PostForm
      // titles: '',
      // body: ''
      page: 1,
      limit: 10,
      totalPages: 0,
      isPostsLoading: false,
      selectedSort: '',
      searchQuery: '',
      sortOptions: [
        {value: 'title', name: 'by name'},
        {value: 'body', name: 'by content'}
      ]
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
      this.myDialogVisible = false
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
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !==post.id)
    },
    showDialog() {
      this.myDialogVisible = true
    },

    async fetchPosts() {
        try {
          this.isPostsLoading = true

            // const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
          // pagination
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _page: this.page,
              _limit: this.limit
            }
          })
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
          this.posts = response.data
            // Add block finally
            // this.isPostsLoading = false


        } catch (error) {
          alert('Error json_placeholder')
        } finally {
          // use without setTimeout
          this.isPostsLoading = false
        }
    },
    changePage(pageNumber) {
      this.page = pageNumber
      // use whach
      // this.fetchPosts()
    },
    // inputBody(event) {
    //   this.body = event.target.value
    // }
  },
  mounted() {
    this.fetchPosts()
  },
  computed: {
    // any name
    sortedPosts(newValue) {
      // no mutation
      return [...this.posts].sort((a,b) => {
        return a[this.selectedSort].localeCompare(b[this.selectedSort])
      })
    },
    // search on sorted Array
    sortedAndSearchesPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },
  watch: {
    page() {
      this.fetchPosts()
    },
    // the function has the same name as the one declared in the component
    selectedSort(newValue) {
      // console.log(newValue)
      // this.posts.sort((a,b) => {
        // mutation
        // return a[this.selectedSort].localeCompare(b[this.selectedSort])
      //   return a[newValue].localeCompare(b[newValue])
      //
      // })
    },
    myDialogVisible(newValue) {
      // console.log(newValue)
    }
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
    .app__buttons {
      margin: 15px 0;
      display: flex;
      justify-content: space-between;
    }
    .page__wrapper {
      display: flex;
      margin-top: 15px;
    }
    .page {
      border: 1px solid black;
      padding: 10px;
      cursor: pointer;
    }
    .current-page {
      border: 2px solid orangered;
    }


</style>