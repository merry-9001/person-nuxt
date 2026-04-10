<script setup lang="ts">
const posts = [
  { id: 'nuxt-demo', title: 'Nuxt 3 Demo 启动说明', summary: '从本地开发到线上部署的最小链路。' },
  { id: 'github-actions', title: 'GitHub Actions 自动部署', summary: 'Push 到 main 后自动构建并发布。' },
  { id: 'server-setup', title: '服务器部署准备', summary: '准备 Node.js、pm2 和部署目录。' }
]
</script>

<template>
  <section class="panel">
    <p class="section-label">Posts</p>
    <h2>文章列表</h2>

    <div class="list">
      <NuxtLink
        v-for="post in posts"
        :key="post.id"
        :to="`/posts/${post.id}`"
        class="list-item"
      >
        <strong>{{ post.title }}</strong>
        <span>{{ post.summary }}</span>
      </NuxtLink>
    </div>
  </section>
</template>
