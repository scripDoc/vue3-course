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
import RComments from './components/r-comments'
import RForm from './components/r-form'
import RResult from './components/r-result'

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
      this.createResumeItems(val)
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
    },
    async createResumeItems(items) {
      const response = await fetch(
        'https://vue3-coursework-2-default-rtdb.firebaseio.com/resume-items.json',
        {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(items)
        }
      )

      const result = await response.json()
      console.log('result', result)
    },
    async fetchResumeItems() {
      try {
        const response = await fetch(
          'https://vue3-coursework-2-default-rtdb.firebaseio.com/resume-items.json'
        )
        const resumeItems = await response.json()

        this.result = Object.keys(resumeItems).map(key => ({ key, ...resumeItems[key] }))
      } catch (error) {
        console.log(error)
      }
    }
  },
  mounted() {
    this.fetchResumeItems()
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
