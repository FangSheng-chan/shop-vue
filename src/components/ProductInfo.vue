<template>
  <el-container>
    <el-header height="100px">
      <el-col :span="12">
        <div class="grid-content bg-purple" align="left">
          <img src="/static/logo.png" width="100px" height="70px">
        </div>
      </el-col>
      <el-col :span="12">
        <div class="grid-content bg-purple-light" align="right">
          <el-button>登陆</el-button>
          <el-button>注册</el-button>
        </div>
      </el-col>
    </el-header>
    <el-main>
      <el-row>
        <el-col :span="8">
          <div class="grid-content bg-purple">
            <img :src="pro.pimg">
          </div>
        </el-col>
        <el-col :span="16">
          <div class="grid-content bg-purple-light">
            <el-row>
              <el-col :span="12">
                <div class="grid-content bg-purple">
                  <h3>商品名称</h3>
                </div>
              </el-col>
              <el-col :span="12">
                <div class="grid-content bg-purple-light">
                  <h3>{{pro.name}}</h3>
                </div>
              </el-col>
            </el-row>
            <el-row>
              <el-col :span="12">
                <div class="grid-content bg-purple">
                  <h3>商品价格</h3>
                </div>
              </el-col>
              <el-col :span="12">
                <div class="grid-content bg-purple-light">
                  <h3>{{pro.price}}元</h3>
                </div>
              </el-col>
            </el-row>

          </div>
          <el-row>
            <el-col :span="24">
              <div class="grid-content bg-purple" style="margin-top: 200px">
                <el-button type="danger" round>点击购买</el-button>
              </div>
            </el-col>
          </el-row>
        </el-col>
      </el-row>

    </el-main>
  </el-container>

</template>

<script>
  export default {
    name: "ProductInfo",
    data() {
      return {
        pid: this.$route.params.pid,
        pro:null

      }
    },
    created() {
      this.getProduct();
    },
    methods: {
      getProduct() {
        var vm = this;
        this.axios({
          method: "GET",
          url: "http://localhost:8090/product/getProductById?fid=" + vm.pid
        }).then(function (response) {
          vm.pro = response.data;
        })
      }
    }
  }
</script>

<style scoped>

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
    padding: 10px 0 10px 10px;
  }

  body > .el-container {
    margin-bottom: 40px;
  }
</style>
