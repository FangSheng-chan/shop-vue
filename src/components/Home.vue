<template>
    <el-container>
      <el-header height="100px">
        <el-col :span="12"><div class="grid-content bg-purple" align="left">
          <img src="/static/logo.png" width="100px" height="70px">
        </div></el-col>
        <el-col :span="12"><div class="grid-content bg-purple-light" align="right">
          <el-button>登陆</el-button>
          <el-button>注册</el-button>
        </div></el-col>
      </el-header>
      <el-main>
        <div class="block">
          <el-carousel height="300px" indicator-position="none">
            <el-carousel-item v-for="item in imgs" :key="item">
              <img :src=item >
            </el-carousel-item>
          </el-carousel>
        </div>

        <div class="products">
          <div v-for="pro in pros" class="product">
            <img :src="pro.pimg">
            <br/>
            <h4>{{pro.pname}}</h4>
            <h4>{{pro.price}}元</h4>
            <el-button type="danger" round @click="gtproinfo(pro.pid)">点击购买</el-button>
          </div>
        </div>
      </el-main>
      <el-footer height="260px"></el-footer>
    </el-container>
</template>

<script>
  export default {
    data(){
      return {
        imgs:[
          "../static/1.jpg",
          "../static/2.jpg",
          "../static/3.jpg",
          "../static/4.jpg"
        ],
        pros: null
      }
    },
    created() {
      this.getList();
    },
    methods:{
      getList:function () {
        var vm = this;
        this.axios({
          method: 'GET',
          url: 'https://www.easy-mock.com/mock/5f6e1391d94dae3ef99d165b/product/list'
        }).then(function (response) {
          vm.pros = response.data.pros;
        })
      },
      gtproinfo(pid){
        this.$router.push("/ProductInfo/"+pid)
      }
    }
  }
</script>

<style scoped>

  .product{
    margin-top: 10px;
    display: inline-block;
    width: 30%;
  }

  .product img{
    width: 250px;
    height: 300px;
  }

  .el-header, .el-footer {
    margin-top: 10px;
    /*background-color: #B3C0D1;*/
    color: #333;
    text-align: center;
    line-height: 60px;
  }

  .el-aside {
    /*background-color: #D3DCE6;*/
    color: #333;
    text-align: center;
    line-height: 200px;
  }

  .el-main {
    /*background-color: #E9EEF3;*/
    color: #333;
    text-align: center;
    /*line-height: 560px;*/
    height: 800px;
    padding: 10px 0 10px  10px;
  }

  body > .el-container {
    margin-bottom: 40px;
  }

</style>

