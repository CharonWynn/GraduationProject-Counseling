<template>
  <div class="section">
    <mt-header title="案例内容" fixed>
      <mt-button icon="back" @click="goback" slot="left"></mt-button>
    </mt-header>
    <div class="section_index">
      <h1 class="title">{{section.title}}</h1>
      <div class="info">
        <div class="left">
          <img src="https://avatars2.githubusercontent.com/u/39826728?s=460&v=4">
          <div>
            <p class="name">{{section.username}}</p>
            <p class="post">身份标签 | {{section.createAt | convertTime('YYYY-MM-DD')}}</p>
          </div>
        </div>
      </div>
      <div class="section_info">
        {{section.content}}
        <!-- <img src="https://avatars2.githubusercontent.com/u/39826728?s=460&v=4"> -->
      </div>
    </div>
  </div>
</template>

<script>
  export default{
    data(){
      return {
        id: this.$route.query.id,
        section: {}
      }
    },
    methods: {
      goback () {
        this.$router.go(-1)
      },
      getSection(){
        return new Promise((resolve, reject) => {
          this.$ajax({
            url: '/case/' + this.id,
            method: 'get'
          }).then(res=>{
            resolve(res)
          }).catch(err=>reject(err))
        })
      }
    },
    created(){
      this.getSection().then(res=>{
        this.section = res.data.data;
      }, err=>console.log(err))
      // this.$ajax({
      //   url: '/api/case/' + this.id,
      //   method: 'get'
      // }).then(res=>{
      //   console.log(res)
      //   this.section = res.data.data;
      // }).catch(err=>console.log(err))
    }
  }
</script>

<style scoped>
  .section >>> .mint-header{
    color: #3e3e3e;
    font-size: 0.9rem;
    background-color: #fbfbfb;
  }

  .section .section_index{
    margin-top: 40px;
    padding: 10px;
    background-color: #fff;
  }
  .section .section_index h1{
    font-weight: 500;
    font-size: 1.4rem;
    margin-top: 0;
  }
  .section .section_index .info{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .section .section_index .info .left{
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-weight: 500;
    font-size: 0.7rem;
    color: #8e8e8e;
  }
  .section .section_index .info .left .name{
    font-size: 0.9rem;
    font-weight: 500;
    color: #333;
  }
  .section .section_index .info .left img{
    width: 40px;
    height: 40px;
    border-radius: 50%;
    margin-right: 10px;
  }

  .section .section_index .section_info{
    margin: 20px 0;
    word-break: break-all;
    font-size: 1rem;
  }
  .section .section_index .section_info img{
    width: 100%;
  }

  .section .section_comment{
    background-color: #fff;
    padding: 8px 8px 0 8px;
    margin-top: 10px;
  }
  .section .section_comment h1{
    font-size: 1rem;
    font-weight: 400;
  }
  .section_send_comment{
    position: fixed;
    bottom: 0;
    width: 100%;

  }
  .section_send_comment >>> .mint-cell-wrapper{
    /* font-size: 1.1rem; */
  }
</style>
