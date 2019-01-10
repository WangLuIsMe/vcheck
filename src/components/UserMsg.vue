<template>
  <div class="usermsg">
    <top :system="system"></top>
    <div class="">
        <img :src="user.useravatar">
        <label>用户昵称：</label>
        <p>{{user.username}}</p>
        <label>手机号：</label>
        <p>{{user.phonenumber}}</p>
        <label>密码：</label>
        <p>{{user.useravatar}}</p>
    </div>
    <foot :system="system"></foot>
  </div>
</template>
<script>
import top from "./Top.vue";
import foot from "./Foot.vue";
export default {
  name: "usermag",
  props: {
    system: Object
  },
  data() {
    return {
        userid:"",
        user:"",
        username:"",
        phonenumber:"",
        userlevel:"",
        useravatar:""
    }
  },
  methods: {
    getuser(){
      this.axios.get('http://www-luluisme.gz01.bdysite.com/api/getUser.php?userid=' + this.userid).then((res)=>{
        this.user = res.data;
        console.log(this.user[0])
        this.username = this.user[0].userName;
        this.phonenumber = this.user[0].phoneNumber;
        this.userlevel = this.user[0].userLevel;
        this.useravatar = this.user[0].userAvatar;
      })
    }
  },
  components: {
    top,
    foot
  },
  created() {
    this.userid = $cookies.get('userId'); 
    this.getuser();
    // this.username = this.user[0].userName;
    // this.phonenumber = this.user[0].phoneNumber;
    // this.userlevel = this.user[0].userLevel;
    // this.useravatar = this.user[0].userAvatar;
    console.log(this.user[0])
    // console.log(this.user[0].userName)
  }
};
</script>
<!-- 添加“作用域”属性以仅将CSS限制在此组件中 -->
<style scoped>

</style>