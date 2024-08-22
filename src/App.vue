<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <my-button
        @click="showDialog" style="margin: 10px 0"
    >Создать пост</my-button>
    <input type="text" v-model.trim="modificatorValue">

    <my-dialog v-model:show="dialogVisible">
    <post-form @create="createPost"/>
    </my-dialog>
    <post-list :posts="posts" @remove="removePost"/>
  </div>
</template>

<script>



import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import MyDialog from "@/components/UI/MyDialog.vue";
import MyButton from "@/components/UI/MyButton.vue";

export default {
  components: {MyButton, MyDialog, PostList, PostForm},



  data() {
    return {
      posts:[
        {id:1, title:'Пост о JS 1', body:'Тело поста 1'},
        {id:2, title:'Пост о JS 2', body:'Тело поста 2'},
        {id:3, title:'Пост о JS 3', body:'Тело поста 3'}
      ],
      dialogVisible: false,
      modificatorValue:"",
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





</style>