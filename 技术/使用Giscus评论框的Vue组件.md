

# 在Vitepress中使用Giscus评论框的Vue组件

在这个教程中，我们将学习如何在Vitepress项目中嵌入Giscus评论框的Vue组件。Giscus是一个强大的评论系统，它允许你在你的文档或博客中轻松添加评论功能。我们将按照以下步骤进行操作。

## 步骤1：创建Vue组件

首先，我们需要创建一个Vue.js组件，该组件将作为Giscus评论框的容器。我们将命名这个组件为 `GiscusComment.vue`。以下是组件的代码：

```vue
<template>
  <div>
    <!-- 这里放置Giscus评论框的容器 -->
    <div ref="giscus"></div>
  </div>
</template>

<script>
export default {
  mounted() {
    // 步骤2：创建一个 script 元素以加载 Giscus 的客户端脚本
    const script = document.createElement('script');
    script.src = 'https://giscus.app/client.js';
    script.async = true;

    // 步骤3：配置 Giscus 评论框参数
    script.setAttribute('data-repo', 'xbrooke/lynk-giscus'); // 设置存储库信息
    script.setAttribute('data-repo-id', 'R_kgDOKkX5JA'); // 设置存储库 ID
    script.setAttribute('data-category', 'Q&A'); // 设置评论类别
    script.setAttribute('data-category-id', 'DIC_kwDOKkX5JM4CaZYg'); // 设置评论类别 ID
    script.setAttribute('data-mapping', 'pathname'); // 设置评论框的映射方式
    script.setAttribute('data-strict', '0'); // 是否启用严格模式
    script.setAttribute('data-reactions-enabled', '1'); // 是否启用回应功能
    script.setAttribute('data-emit-metadata', '0'); // 是否发布元数据
    script.setAttribute('data-input-position', 'bottom'); // 评论输入框位置
    script.setAttribute('data-theme', 'preferred_color_scheme'); // 主题设置
    script.setAttribute('data-lang', 'zh-CN'); // 语言设置
    script.crossOrigin = 'anonymous';

    // 步骤4：当脚本加载完成后，渲染 Giscus 评论框
    script.onload = () => {
      // Giscus 配置参数
      const giscusConfig = {
        repo: 'GitHub名/仓库名', // 你的存储库名
        repoID: 'R_kgDOKxxxxx', // 你的存储库 ID
        mapping: 'pathname', // 映射方式
        category: 'Q&A', // 评论类别
      };

      // 创建 Giscus 评论框并渲染到容器中
      new Giscus(giscusConfig).render(this.$refs.giscus);
    };

    // 步骤5：将 script 元素添加到组件的容器中
    this.$refs.giscus.appendChild(script);
  },
};
</script>
```

确保替换上述代码中的存储库信息和其他配置参数以适应你的需求。



## 步骤2：在Vitepress中使用Vue组件

1. 在你的Markdown文件中，确保你启用了评论功能，这可以通过YAML头信息来实现：

```
markdownCopy code---
comment: true
---

# 我的页面标题

欢迎来到我的页面！

<!-- 步骤6：插入Giscus评论框组件 -->
<GiscusComment />
```

1. 安装Vue.js依赖，如果你还没有安装的话：

```
bashCopy code
npm install vue
```

## 步骤3：运行Vitepress

保存你的文件并重新启动Vitepress本地开发服务器。现在，你的页面应该显示了Giscus评论框，允许读者与你的内容互动。

这就是如何在Vitepress项目中嵌入Giscus评论框的完整教程。希望这对你有所帮助，让你的文档或博客更加互动和有趣！