<template>
  <div class="card card-w70">
    <h3 v-if="!result.length">Добавьте первый блок, чтобы увидеть результат</h3>

    <component
      v-else
      v-for="{ key, blockType, content } in result"
      v-bind="{ content }"
      :is="blockType"
      :key="key"
    ></component>
  </div>
</template>

<script>
import Title from './title.vue'
import Subtitle from './subtitle.vue'
import Avatar from './avatar.vue'
import Text from './text.vue'

export default {
  components: { Title, Subtitle, Avatar, Text },
  name: 'RResult',
  props: {
    result: { type: Array, default: () => [] }
  }
}
</script>
