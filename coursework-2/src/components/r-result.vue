<template>
  <div class="card card-w70">
    <h3 v-if="!result.length">Добавьте первый блок, чтобы увидеть результат</h3>

    <div
      v-else
      v-for="(item, idx) in result"
      v-html="getTemplate(item)"
      :key="idx + item.blockType"
      :class="['block', item.blockType]"
    ></div>
  </div>
</template>

<script>
export default {
  name: 'RResult',
  props: {
    result: { type: Array, default: () => [] }
  },
  methods: {
    getTemplate({ blockType, content }) {
      switch (blockType) {
        case 'title':
          return `<h1>${content}</h1>`
        case 'subtitle':
          return `<h2>${content}</h2>`
        case 'avatar':
          return `<img src="${content}" />`
        case 'text':
          return `<p>${content}</p>`
        default:
          return `<h1>Такого блока не существует</h1>`
      }
    }
  }
}
</script>
