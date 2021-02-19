<template>
 

  <el-container class="home-container">
    <!-- 头部区域 -->
  <el-header>
    <div>
      <img src="../assets/NIke.png" alt="">
      <span>体育用品购物平台系统</span>
    </div>
    <el-button type="info" @click="logout">退出</el-button>
  </el-header>
  <!-- 页面主体 -->
  <el-container>
    <!-- 侧边栏 -->
    <el-aside width="200px">
      <!-- 侧边栏菜单 -->
      <el-menu background-color="#333744" text-color="#fff"
      active-text-color="#ffd04b">
      <!-- 一级菜单 -->
      <el-submenu :index="item.id + '' " v-for="item in menulist" :key='item.id'>
        <!-- 一级菜单模板区域 -->
        <template slot="title">
          <!-- 图标 -->
          <i class="el-icon-location"></i>
          <!-- 文本 -->
          <span>{{item.authName}}</span>
        </template>
        
        <!-- 二级菜单 -->
          <el-menu-item :index="subItem.id + '' " v-for="subItem in item.children"
          :key="subItem.id">
            <template slot="title">
          <!-- 图标 -->
          <i class="el-icon-location"></i>
          <!-- 文本 -->
          <span>{{subItem.authName}}</span>
        </template>
          </el-menu-item>
          
        </el-submenu>
     
      
    </el-menu>
    </el-aside>
    <!-- 右侧内容 -->
    <el-main>Main</el-main>
  </el-container>
</el-container>

</template>

<script>
export default {
  data(){
    return{
      // 左侧菜单数据
      menulist: []
    }
  },
  created(){
    this.getMenuList()
  },
  methods:{
    logout(){
      // 清空token
      window.sessionStorage.clear()
      // 跳转
      this.$router.push('/login')
    },
    // 获取菜单
    async getMenuList(){
     const {data : res} = await this.$http.get('menus')
     if(res.meta.status !== 200) return this.$message.error(res.meta.msg)
     this.menulist = res.data
     console.log(res);
    }
  }
}
</script>

<style lang="less" scoped>
.home-container{
  height: 100%;
}

.el-header {
  background-color: #f5f5f5;
  display: flex;
  justify-content: space-between;
  padding-left: 0;
  align-items: center;
  font-size: 20px;
  > div {
    display: flex;
    align-items: center;
    span {
      margin-left: 15px;
    }
  }
}

// .el-header img{
//   height: 58px;
// }

.el-aside {
  background-color: #333744;
}

.el-main {
  background-color: #eaedf1;
}
</style>