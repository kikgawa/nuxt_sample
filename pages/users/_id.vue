<template>
  <section class="container">
    <div>
      <h3>{{ user.id }}</h3>
      <img :src="user.profile_image_url" width="120" alt="" />
      {{ user.id }}さんの投稿一覧
      <ul>
        <li v-for="item in items" :key="item.id">
          <h4>{{ item.title }}</h4>
          <div>{{ item.body.slice(0, 130) }}....</div>
          <p>
            <a target="_blank" :href="item.url">{{ item.url }}</a>
          </p>
        </li>
      </ul>
      <p>
        <nuxt-link to="/axios">axiosサンプルページへ戻る</nuxt-link>
      </p>
    </div>
  </section>
</template>
<script>
export default {
  async asyncData({ route, app }) {
    const user = await app.$axios.$get(
      `https://qiita.com/api/v2/users/${route.params.id}`
    )
    const items = await app.$axios.$get(
      `https://qiita.com/api/v2/items?query=user:${route.params.id}`
    )
    return { user, items }
  },
}
</script>
