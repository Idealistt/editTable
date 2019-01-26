<template>
  <div id="app">
        <div  class="about">
            <editTable/>
        </div>
  </div>
</template>

<script>
import editTable from './components/editTable.vue'
export default {
  name: 'app',
  components: {
      editTable
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.about{
    display: inline-block;
}
.el-row{
    padding: 25px;
}
</style>
