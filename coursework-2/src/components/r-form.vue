<template>
  <form class="card card-w30" @submit.prevent="submitHandler">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="blockType">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" rows="3" v-model="content"></textarea>
    </div>

    <button class="btn primary" :disabled="content.length < 4">Добавить</button>
  </form>
</template>

<script>
export default {
  name: 'RForm',
  emits: ['add'],
  data: () => ({
    blockType: 'title',
    content: ''
  }),
  methods: {
    submitHandler() {
      this.$emit('add', {
        blockType: this.blockType,
        content: this.content
      })
      this.blockType = 'title'
      this.content = ''
    }
  }
}
</script>
