<template>
  <div class="app">
    <h1>Страница с постами</h1>

    <my-input v-model="searchQuery" placeholder="Найти пост по заголовку..."/>

    <div class="app__btns">
      <my-button
          @click="showDialog"
      >Создать пост</my-button>
      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      />
    </div>

    <my-button @click="getAllPosts">Получить посты</my-button>

    <my-dialog v-model:show="dialogVisible">
    <post-form @create="createPost"/>
    </my-dialog>
    <post-list :posts="sortedAndSearch" @remove="removePost" v-if="!isPostLoading"/>
    <div v-else>Идет загрузка...</div>
  </div>
</template>

<script>



import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import MyDialog from "@/components/UI/MyDialog.vue";
import MyButton from "@/components/UI/MyButton.vue";
import axios from "axios";
import MySelect from "@/components/UI/MySelect.vue";
import MyInput from "@/components/UI/MyInput.vue";
import * as sea from "node:sea";

export default {
  components: {MyInput, MySelect, MyButton, MyDialog, PostList, PostForm},



  data() {
    return {
      posts:[],
      dialogVisible: false,
      isPostLoading: false,
      searchQuery:String,
      selectedSort: '',
      sortOptions: [

        {value:'title', name:'По описанию'},
        {value:'body', name:'По содержанию'},
      ]
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async getAllPosts() {
      try {
        this.isPostLoading = true
        setTimeout( async () => {
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
        this.posts = response.data
          this.isPostLoading = false
        }, 100)
      } catch (e) {
        alert(e)
      }
    },
  },
  mounted() {
    this.getAllPosts();
  },


  computed: {
    sea() {
      return sea
    },
    sortedPosts() {

      return [...this.posts].sort((post1, post2) => {
        return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
      })
  },
    sortedAndSearch() {
      return this.sortedPosts.filter(post => post.title.includes(this.searchQuery))
    }
  }

}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  .app {
    padding: 10px;
  }

  .app__btns {
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
  }





</style>