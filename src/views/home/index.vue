<template>
  <div class="content">
    <el-container>
      <el-aside width="200px">

      </el-aside>
      <el-container>
        <el-header>Header</el-header>
        <el-main>Main</el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
export default {
  name: 'frist',
  data () {
    return {}
  }
}
</script>

<style lang='less' scoped>
body {
  padding: 0;
  margin: 0;
  overflow: hidden;
}
.content {
  overflow-x: hidden;
  width: 100%;
  height: 110vh;
  background-image: url(../../assets/123.webp);
  display: flex;
  flex-direction: row;
}
.el-aside {
  background-color: rgb(53, 59, 78);
  overflow: auto;
  color: black;
  min-height: 100vh;
  box-sizing: border-box;
  flex-shrink: 0;
}
.el-header {
  width: 100vw;
  background-color: skyblue;
}
section {
  flex: 1;
  // flex-direction: column;
}
</style>
