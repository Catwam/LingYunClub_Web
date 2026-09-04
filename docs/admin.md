<script setup>
import AdminPanel from './.vitepress/components/admin/AdminPanel.vue'
import ToastHost from './.vitepress/components/ui/ToastHost.vue'
</script>

# 管理后台

::: tip 纯前端说明
本后台没有后端：所有增删改即时暂存在当前浏览器（localStorage）。
要正式发布内容，请在「数据发布」标签导出 JSON 文件，替换
`docs/.vitepress/data/site-data.json` 后重新构建。
:::

<AdminPanel />
<ToastHost />
