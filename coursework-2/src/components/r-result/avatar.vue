<template>
  <div class="avatar">
    <img :src="imgUrl" @error="imgUrl = defaultImgUrl" />
  </div>
</template>

<script>
export default {
  data: () => ({
    imgUrl: '',
    defaultImgUrl:
      'https://cdn.dribbble.com/users/5592443/screenshots/14279501/drbl_pop_r_m_rick_4x.png'
  }),
  mounted() {
    this.imgUrl = this.$attrs.content
  }
}
</script>
