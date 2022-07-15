<template>
  <div>
    <div class="mb-10">
      <v-btn @click="getIp">IPアドレスを取得</v-btn>
      <p>{{ ip }}</p>
    </div>
    <div>
      <v-btn @click="getQiita">Qiita Nuxtタグを取得</v-btn>
      <ul>
        <li v-for="item in items" :key="item.id">
          {{ item.title }}
          <div>{{ item.body.slice(1, 100) }}...</div>
          <a :href="item.url">{{ item.url }}</a>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      ip: '',
      items: [],
    }
  },
  methods: {
    async getIp() {
      this.ip = await this.$axios.$get('http://icanhazip.com')
    },
    async getQiita() {
      this.items = await this.$axios.$get(
        'https://qiita.com/api/v2/items?query=tag:nuxt.js'
      )
    },
  },
}
</script>
