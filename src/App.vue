<template>
  <div id="app">
    <h1>Список задач <like-button :likes.sync="headerLikes" /></h1>
    <h3>Количество лайков - {{ countLikes }}</h3>

    <form class="form" @submit.prevent="addTask">
      <input placeholder="Введите текст" v-model="message">
      <button type="submit" title="Добавить задачу">Добавить</button>
      <like-button :likes.sync="formLikes" />
    </form>

    <div v-if="uncompletedTasks.length === 0">Вы великолепны!</div>
    <div v-else-if="uncompletedTasks.length === 1">Остался последний рывок!</div>
    <div v-else>Осталось сделать задач: <span class="counter">{{ uncompletedTasks.length }}</span></div>

    <div class="flex">
      <tasks-list :tasks="uncompletedTasks" title="Текущие задачи"/>
      <tasks-list :tasks="completedTasks" title="Завершенные задачи"/>
    </div>

    <transition name="rotate">
      <img src="https://pbs.twimg.com/media/BG2zfl6CEAEWL3B.jpg" alt="" v-show="uncompletedTasks.length === 0">
    </transition>
  </div>
</template>

<script>
import LikeButton from '@/components/LikeButton'
import TasksList from '@/components/TasksList'
import tasks from '@/data/tasks'

export default {
  name: 'App',
  components: {
    LikeButton,
    TasksList
  },
  data: () => ({
    message: '',
    headerLikes: 2,
    formLikes: 4,
    tasks
  }),
  methods: {
    addTask () {
      if (this.message === '') {
        return false
      }

      this.tasks.push({
        text: this.message,
        done: false,
        likes: 0,
        dislikes: 0
      })
      this.message = ''
    }
  },
  computed: {
    completedTasks () {
      return this.tasks.filter(task => task.done)
    },
    uncompletedTasks () {
      return this.tasks.filter(task => !task.done)
    },
    countLikes () {
      return this.headerLikes + this.formLikes + this.tasks.reduce((value, task) => value + task.likes, 0)
    }
  }
}
</script>

<style lang="stylus">
.flex
  display flex

.form
  margin 20px 0

.rotate
    &-enter
    &-leave-to
        transform rotateY(360deg) scale(1.5)
        opacity 0

    &-enter-active
    &-leave-active
        transition .5s

.stretching
    &-enter
    &-leave-to
        width 0
        opacity 0

    &-enter-active
    &-leave-active
        transition .5s

</style>
