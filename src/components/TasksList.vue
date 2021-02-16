<template>
  <transition name="stretching">
    <div v-show="tasks.length != 0" class="block">
      <h2 v-if="title">{{ title }}</h2>
      <div class="list">
        <div class="item" :class="{done: task.done}" v-for="task in tasks" :key="task.text">
          <input type="checkbox" v-model="task.done" >
          {{ task.text }}
          <like-button :likes.sync="task.likes" />
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import LikeButton from '@/components/LikeButton'

export default {
  components: {
    LikeButton
  },
  props: {
    tasks: Array,
    title: String
  }
}
</script>

<style lang="stylus">
.block
  width 100%
  transition .3s linear

.list
  padding 20px
  border 1px solid #ccc
  margin 20px 0

.item
  margin 10px 0

.done
  text-decoration line-through

</style>
