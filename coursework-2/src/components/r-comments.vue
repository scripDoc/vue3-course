<template>
  <div v-if="loading" class="loader"></div>
  <p v-else-if="!comments.length">
    <button class="btn primary" @click="$emit('load')">Загрузить комментарии</button>
  </p>
  <div v-else class="card">
    <h2>Комментарии</h2>
    <ul class="list">
      <li class="list-item">
        <div>
          <p><strong>test@microsoft.com</strong></p>
          <small>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi, reiciendis.
          </small>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'RComments',
  emits: ['load'],
  props: {
    comments: { type: Array, default: () => [] },
    loading: { type: Boolean, default: false }
  }
}
</script>
