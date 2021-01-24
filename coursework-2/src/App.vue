<template>
  <div>
    <div class="container column">
      <r-form @add="addHandler"></r-form>
      <r-result :result="result"></r-result>
    </div>
    <div class="container">
      <r-comments :comments="comments" :loading="loading" @load="fetchComments"></r-comments>
    </div>
  </div>
</template>

<script>
import RComments from './components/r-comments.vue'
import RForm from './components/r-form.vue'
import RResult from './components/r-result.vue'

export default {
  components: { RForm, RResult, RComments },
  data: () => ({
    result: [],
    comments: [],
    loading: false
  }),
  methods: {
    addHandler(val) {
      this.result.push(val)
    },
    async fetchComments() {
      try {
        this.loading = true
        const response = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42')
        this.comments = await response.json()
        this.loading = false
      } catch (error) {
        console.log(error)
        this.loading = false
      }
    }
  }
}
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
