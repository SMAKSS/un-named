<template>
  <div v-if="render">
    <vue-json-pretty :data="profile" showLength/>
  </div>
  <div
    v-else
    class="row bg-grey-2 full-width justify-center items-center __spinner"
  >
    <q-spinner color="primary" size="3em" :thickness="2" />
  </div>
</template>

<script>
import VueJsonPretty from 'vue-json-pretty'
export default {
  name: 'public-profile',
  components: {
    VueJsonPretty
  },
  data() {
    return {
      render: false,
      profile: {}
    }
  },
  async mounted() {
    const { id } = this.$router.currentRoute.params
    this.profile = await this.$api.getPublicProfile(id)
    this.render = true
  }
}
</script>

<style lang="scss" scoped>
.__spinner {
  height: 100vh;
}
</style>