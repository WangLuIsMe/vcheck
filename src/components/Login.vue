<template>
  <div class="register">
    <!-- <Top :system="system"></Top> -->
      <div class="main">
          <h1>0910聊天室登陆</h1>
          <form>
              <div class="form-group">
                <label for="email">用户昵称：</label>
                <input v-model="username">
              </div>
              <div class="form-group">
                <label for="pwd">密码：</label>
                <input v-model="password" type="password">
              </div>
              <button @click="login($event)">登陆</button>    
              <div id="error">{{error}}</div>
          </form>
      </div>
    <foot :system="system"></foot>
  </div>
</template>

<script>
// import top from './Top.vue'
import foot from './Foot.vue'
export default {
  name: 'login',
  props: {
    system: Object
  },
  data(){
     return {
       msg:"欢迎您来到Vue.js的世界",
       username:"",
       password:"",
       error:"",
     }
  },
  components: {
    foot
  },
  methods:{
    login(){
      event.preventDefault();
this.axios({
 method:"post",
 url:"http://www-luluisme.gz01.bdysite.com/api/loginSave.php",
 data:this.qs.stringify({
  send:1,
  username:this.username,
  password:this.password
 })
}).then((res)=>{
  if (res.data.valid == true){
  this.$router.push({path:'/'})
  }
  if (res.data.valid == false){
  this.error = res.data.message
  }
})
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .main{
    width: 600px;
    margin:50px auto;
  }
  .main h1{
    font-size: 40px;
    color: #333;
    font-weight: 500;
    color: rgb(53, 73, 94);
    text-align: center;
  }
  .main label{
    display: block;
  }
  .main form{
    color:#666;
    font-size: 20px;
    margin-top: 50px;
  }
  .main input{
    border-radius: 5px;
    height:35px;
    line-height: 35px;
    padding:0 15px;
    border:1px solid darkgray;
    width: 100%;
    margin: 10px auto;
  }
  .form-check-input{
    width: 20px;
    height: 18px;
    margin-top: 15px;
  }
  button{
    padding: 10px 20px;
    background-color: rgb(65, 184, 131);
    border: darkgray;
    color: #fff;
    margin-top: 10px;
    border-radius: 5px;
  }
  #error{
    color:red;
    font-size: 20px;
    padding: 7px 0;
    height: 26px;
  }
  footer{
    position: absolute;
    bottom: 0;
  }
</style>
