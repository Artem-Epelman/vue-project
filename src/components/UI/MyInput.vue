<script>
export default {
  name: "my-input",
  props: {
    value: [String, Number],
    placeholder: {
      type: String,

    }
  },
  methods :{
    updateInput(e) {
      this.$emit('update:value', e.target.value);
    }
  }
}
</script>

<template>
  <input type="text" :value="value" @input="updateInput" :placeholder="placeholder"/>
  <slot></slot>
</template>

<style scoped>
input {
  width: 100%;
  margin-top: 15px;
  border: 1px solid teal;
  padding: 10px 15px;
}
</style>