<template>
  <div>
    <el-breadcrumb separator="/">
      <el-breadcrumb-item to="/admin/list">Посты</el-breadcrumb-item>
      <el-breadcrumb-item>{{ $route.params.id }}</el-breadcrumb-item>
    </el-breadcrumb>
    Post {{ $route.params.id }}</div>
</template>

<script>
export default {
  layout: 'admin',
  middleware: ['admin-auth']
}
</script>

<style lang="scss" scoped>

</style>
