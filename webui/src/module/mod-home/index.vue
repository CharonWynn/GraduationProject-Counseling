<template>
  <div class="home">
    <!-- 轮播 -->
    <mt-swipe :auto="4000">
      <mt-swipe-item v-for="(img,index) in imgs" :key="index">
        <img :src="img">
      </mt-swipe-item>
    </mt-swipe>

    <!-- 导航 -->
    <ul class="navbar">
      <li>
        <router-link to="/psycal">
          <img src="@/assets/imgs/navbar/PsyTest.png">
          <div>心理测试</div>
        </router-link>
      </li>
      <li>
        <router-link to="/expert/list">
          <img src="@/assets/imgs/navbar/ExpertCon.png">
          <div>专家咨询</div>
        </router-link>
      </li>
      <li>
        <router-link to="/forum/release">
          <img src="@/assets/imgs/navbar/Topic.png">
          <div>话题发布</div>
        </router-link>
      </li>
      <li>
        <router-link to="/case">
          <img src="@/assets/imgs/navbar/CaseQuery.png">
          <div>案例查询</div>
        </router-link>
      </li>
    </ul>

    <!-- 主页内容列表部分 -->
    <div class="home-list">
      <div class="title">
        <div class="right">
          <img src="">
          <span>专家推荐</span>
        </div>
        <div class="left">
          <router-link to="expert/list">更多 ></router-link>
        </div>
      </div>
      <div class="content">
        <mod-home-list :experts="experts"></mod-home-list>
      </div>
    </div>
  </div>
</template>

<script>
  /**
   * 首页
   */
  export default {
    name: "index",
    data () {
      return {
        imgs: ['http://img2.xiazaizhijia.com/walls/20140829/1440x900_89a2554a1241c64.jpg', 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1555700606910&di=4fdd7fba07998b76d6cc4be3ae1ddb72&imgtype=0&src=http%3A%2F%2Fa3.att.hudong.com%2F01%2F84%2F300000309206129367846097752.jpg'], //轮播图数据
        experts: []
      }
    },
    created () {
      this.$store.dispatch('setUserInfo');
      this.$ajax({
        method: 'get',
        url: '/user/user/type/2'
      }).then(({data}) => {
        this.experts = data.data.list;
      });
    },
  }
</script>

<style scoped>
  .home{
    background-color: #f7f7f7;
  }
  .mint-swipe{
    height: 150px;
  }
  .mint-swipe img{
    width: 100%;
    height: 100%;
  }
  .home >>> .mint-swipe-indicators .mint-swipe-indicator{
    background-color: transparent;
    opacity: .8;
    width: 7px;
    height: 7px;
    border: 1px solid #fff;
  }
  .home >>> .mint-swipe-indicators .is-active{
    background-color: #fff;
  }
  .navbar{
    display: flex;
    text-align: center;
    justify-content: space-around;
    background-color: #fff;
    padding: 20px 0;
  }
  .navbar li{
    flex: 1;
  }
  .navbar li a{
    color: #3e3c3d;
    font-size: 0.8rem;
  }
  .navbar li a img{
    width: 25px;
    height: 25px;
    margin-bottom: 6px;
  }

  .home-list{
    margin-top: 10px;
    background: #fff;
  }
  .title{
    padding: 10px 20px;
    line-height: 30px;
    display: flex;
    justify-content: space-between;
  }
  .title .right{
    color: #3e3c3d;
    font-weight: 600;
  }
  .title .left a{
    font-size: 0.8rem;
    color: #7f7f80;
  }

</style>
