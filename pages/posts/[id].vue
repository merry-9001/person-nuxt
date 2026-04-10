<script setup lang="ts">
const route = useRoute()

const postMap: Record<string, { title: string; content: string }> = {
  'nuxt-demo': {
    title: 'Nuxt 3 Demo 启动说明',
    content: '执行 npm install 和 npm run dev 后，即可在本地启动这个示例项目。'
  },
  'github-actions': {
    title: 'GitHub Actions 自动部署',
    content: '推送到 main 分支时，工作流会安装依赖、构建 .output，并同步到服务器。'
  },
  'server-setup': {
    title: '服务器部署准备',
    content: '服务器需要提前安装 Node.js 和 pm2，并创建好项目部署目录。'
  }
}

const post = computed(() => {
  const id = String(route.params.id)

  return postMap[id] ?? {
    title: '未找到文章',
    content: `当前没有 slug 为 "${id}" 的文章，你可以继续扩展这个动态页面。`
  }
})
</script>

<template>
  <section class="panel">
    <p class="section-label">Post Detail</p>
    <h2>{{ post.title }}</h2>
    <p class="lead">{{ post.content }}</p>

    <div class="actions">
      <NuxtLink class="button secondary" to="/posts">返回列表</NuxtLink>
      <NuxtLink class="button primary" to="/">回到首页</NuxtLink>
    </div>
  </section>
</template>
