<script>



import MyButton from "@/components/UI/MyButton.vue";

export default {
  components: {MyButton},


  props:{
    post: {
      type: Object,
      required: true
    }

  }
}

</script>

<template>
  <div class="post">
  <div>
    <div><strong>Название: </strong>{{post.title}}</div>
    <div><strong>Описание: </strong>{{post.body}}</div>
  </div>
    <div class="post__btns">
      <my-button @click="$emit('remove', post)"
      >Удалить</my-button>
    </div>

  </div>
</template>

<style>


.post  {
  margin-top: 10px;
  padding: 15px;
  border: 2px solid teal;
  display: flex;
  align-items: center;
  justify-content: space-between;
}



</style>