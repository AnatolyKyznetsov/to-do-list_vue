<template>
  <div class="like-button">
    <button type="button" @click="increment">&#9829; {{ likes }}</button>
  </div>
</template>

<script>
export default {
  props: {
    likes: Number
  },
  methods: {
    increment () {
      this.$emit('update:likes', this.likes + 1)
    }
  }
}
</script>

<style lang="stylus">
.like-button
  margin-left 10px
  display inline-block

</style>
