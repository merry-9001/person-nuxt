<script setup lang="ts">
const highlights = [
  'Nuxt 3 路由开箱即用',
  '支持静态页面和动态详情页',
  '已预留 GitHub Actions 自动部署流程'
]
</script>

<template>
  <section class="panel">
    <p class="section-label">Home</p>
    <h2>从这里开始搭你的线上 demo</h2>
    <p class="lead">
      这个页面展示首页内容，你可以继续在 <code>pages/</code> 下扩展业务页面。
    </p>

    <div class="grid">
      <article
        v-for="item in highlights"
        :key="item"
        class="card"
      >
        {{ item }}
      </article>
    </div>

    <div class="actions">
      <NuxtLink class="button primary" to="/posts">查看文章列表</NuxtLink>
      <NuxtLink class="button secondary" to="/about">了解项目结构</NuxtLink>
    </div>
  </section>
</template>
