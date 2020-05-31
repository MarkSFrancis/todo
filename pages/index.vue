<template>
  <div class="container">
    <header>
      <div>
        <logo />
        <h1 class="title">
          todo
        </h1>
      </div>
    </header>

    <tasks />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Logo from '~/components/Logo.vue'
import Tasks from '~/components/Tasks.vue'

export default Vue.extend({
  components: {
    Logo,
    Tasks
  }
})
</script>

<style lang="scss" scoped>
header {
  display: flex;
  justify-content: center;
  text-align: center;
}

.title {
  display: block;
  font-weight: 300;
  font-size: 8rem;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
