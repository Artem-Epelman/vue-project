<template>
  <form @submit.prevent>
    <h4>Cоздание поста</h4>

    <my-input
        v-model:value="post.title"
        @input="post.title=$event.target.value"
        type="text"
    />
    <my-input
        v-model:value="post.body"
        @input="post.body=$event.target.value"
        type="text"
    />

    <my-button
        class="btn"
        style="align-self:flex-end; margin-top: 10px;"
        @click="createPost">Создать</my-button>



  </form>

</template>


<script>
import MyButton from "./UI/MyButton.vue";
import MyInput from "@/components/UI/MyInput.vue";
 export default {
   components : {
     MyInput,
    MyButton
   },

   data() {
     return {
       post: {
         title:'',
         body:'',
       }
     }
   },
   methods: {
     createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post);
      this.post = {
       title: '',
       body: ''
       }
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