---
title: HackerNews 克隆
type: examples
order: 10
---

<<<<<<< HEAD
> 这是 HackerNews 的克隆，建立在 HN 官方的 Firebase API 上，并且使用 Webpack + vue-loader 构建。
=======
> This is a HackerNews clone built upon HN's official Firebase API, Vue 2.0 + vue-router + vuex, with server-side rendering.
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

{% raw %}
<div style="max-width:600px">
  <a href="https://github.com/vuejs/vue-hackernews-2.0" target="_blank">
    <img style="width:100%" src="/images/hn.png">
  </a>
</div>
{% endraw %}

> [Live Demo](https://vue-hn.now.sh/)
> Note: the demo may need some spin up time if nobody has accessed it for a certain period.
>
> [[Source](https://github.com/vuejs/vue-hackernews-2.0)]

## Features

- Server Side Rendering
  - Vue + vue-router + vuex working together
  - Server-side data pre-fetching
  - Client-side state & DOM hydration
- Single-file Vue Components
  - Hot-reload in development
  - CSS extraction for production
- Real-time List Updates with FLIP Animation

## Architecture Overview

<img width="973" alt="Hackernew clone architecture overview" src="/images/hn-architecture.png">
