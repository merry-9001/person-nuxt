<template>
  <div class="shell">
    <header class="hero">
      <div>
        <p class="eyebrow">Nuxt 3 Demo</p>
        <h1>一个可直接接入 CI/CD 的最小示例</h1>
        <p class="subtitle">
          包含多页面跳转、动态路由，以及通过 GitHub Actions 自动部署到服务器的基础流程。
        </p>
      </div>

      <nav class="nav">
        <NuxtLink to="/">首页</NuxtLink>
        <NuxtLink to="/about">关于</NuxtLink>
        <NuxtLink to="/posts">文章</NuxtLink>
      </nav>
    </header>

    <main class="content">
      <slot />
    </main>
  </div>
</template>
