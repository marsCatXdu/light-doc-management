<template>
  <div class="layout">
    <el-container class="container">
      <el-aside 
        :class="{'aside-collapsed': isCollapse==true,
                 'aside-expand': isCollapse==false}"
      >
        <div class="head">
          <fold class="menu-icon" v-if="!isCollapse" @click="toggleMenu()" />
          <expand class="menu-icon" v-if="isCollapse" @click="toggleMenu()" />
          <span v-if="!isCollapse">Management Demo</span>
        </div>
        <div class="line" />
        <el-menu
          background-color="#222832"
          text-color="#fff"
          :router="true"
          :collapse="isCollapse"
          :collapse-transition="false"
        >
          <el-sub-menu index="1">
            <template #title>
              <el-icon>
                <histogram class="menu-icon" />
              </el-icon>
              <span class="menu-text">Main Functions</span>
            </template>
            <el-menu-item-group title="Main Functions Group">
              <el-menu-item index="/"><i class="el-icon-data-line" />Overview</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
          <el-menu-item index="/about">
            <el-icon><document /></el-icon>
            <span>about Page</span>
          </el-menu-item>
        </el-menu>
      </el-aside>
      <el-container class="content">
        <Header />
        <div class="main">
          <router-view />
        </div>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import { Fold, Expand, Histogram, Document } from '@element-plus/icons-vue'

export default {
  name: 'App',
  components: {
    Header,
    Fold,
    Expand,
    Histogram,
    Document
  },
  data() {
    return {
      isCollapse: false
    }
  },
  methods: {
    toggleMenu: function() {
      this.isCollapse = !this.isCollapse;
      console.log("toggle!~");
    }
  }
}
</script>

<style scoped>
.layout {
  min-height: 100vh;            /* 1vh 等于页面高度的 1% */
  background-color: #ffffff;
}

.container {
  height: 100vh;
}

.aside-expand {
  width: 230px!important;
  background-color: #222832;
}

.aside-collapsed {
  width: fit-content;
  background-color: #222832;
}

.head {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 50px;
}

.head > div {
  display: flex;
  align-items: center;
}

.head el-icon {
  width: 50px;
  height: 50px;
  margin-right: 10px;
}

.menu-icon {
  width: 24px;
  height: 24px;
  color: #ffffff;
}

.menu-text {
  margin-left: 8px;
}

.head span {
  font-size: 16px;
  margin-left: 8px;
  margin-bottom: 2px;
  color: #ffffff;
}

.line {
  border-top: 1px solid hsla(0, 0%, 100%, .05);
  border-bottom: 1px solid rgba(0, 0, 0, .2);
}

.content {
  display: flex;
  flex-direction: column;
  max-height: 100vh;
  overflow: hidden;
}

.main {
  height: calc(100vh - 100px);
  overflow: auto;
  padding: 10px;
}
</style>

<style>
body {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.el-menu {
  border-right: none!important;
}

.el-sub-menu {
  border-top: 1px;
  border-bottom: 1px solid rgba(0, 0, 0, .2);
}

.el-sub-menu:first-child {
  border-top: none;
}

.el-sub-menu [class^="el-icon-"] {
  vertical-align: -1px!important;
}

a {
  color: #409eff;
  text-decoration: none;
}

.el-pagination {
  text-align: center;
  margin-top: 20px;
}

.el-popper__arrow {
  display: none;
}

</style>
