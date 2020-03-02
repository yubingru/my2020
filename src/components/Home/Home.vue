<template>
  <el-container>
    <el-header>Header</el-header>
    <el-container>
      <el-aside width="200px">Aside</el-aside>
      <el-main>Main</el-main>
    </el-container>
  </el-container>
</template>
<script></script>
<style scoped>
.el-container {
  height: 100%;
}
.el-header {
  background-color: rgba(116, 86, 0, 0.2);
}
.el-aside {
  background-color: rgb(221, 252, 192);
}
.el-main {
  background-color: rgb(236, 250, 173);
}
</style>
