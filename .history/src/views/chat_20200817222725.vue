<template>
<div class="box">
  <div class="container">
    <div class="left" v-if="userlist.length>0">

      <div class="username" v-for="(item,index) in userlist" :key="index">
        <div class="avatar">
          <img :src="item.avatar" alt="">
        </div>
        <div class="username-text">
          {{item.username}}
        </div>
      </div>

    </div>
    <div class="right">
      <div class="top">聊天室()</div>
      <div class="line"></div>

      <div class="content">

      </div>
      <div class="bottom"></div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: "",
  props: {},
  components: {},
  data() {
    return {
      value: "",
      delUser: "",
      userlist: [],
    };
  },
  methods: {
    send() {
      this.$socket.emit("sendMessage", this.value);
    },
  },
  mounted() {
    this.userlist = JSON.parse(this.$route.params.userlist)
    console.log(JSON.parse(this.$route.params.userlist));
  },
  sockets: {
    loginSuccess(data) {
      if (data.msg !== "登陆失败") {
        this.$router.push({
          name: "chat",
        });
      }
    },
    loginError(data) {
      console.log(data);
    },
    receiveMessage(data) {
      console.log(data);
    },
    userList(data) {
      this.userLists = data;

      console.log(this.userLists);
    },
    delUser(data) {
      console.log(data.username);
    },
  },
  watch: {
    // 'delUser'(val){
    //   console.log(val);
    // }
  },
  computed: {},
};
</script>

<style lang="scss" scoped>
.avatar {
  width: 40px;
  height: 40px;
  margin-left: 20px;
}

.username-text {
  margin-left: 20px;
}

.avatar img {
  width: 100%;
  height: 100%;
}

.bottom {

  height: 140px;
  border: 2px solid green;
  width: 100%;

}

.content {

  height: 320px;
  width: 100%;

  display: flex;

}

.line {
  width: 80%;
  height: 1px;
  background: gray;
  margin-top: 10px;
  margin-bottom: 10px;
}

.top {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 60px;
}

.container {
  display: flex;
  width: 60%;
  height: 550px;
}

.left {
  width: 25%;
  height: 550px;
  background: #2e3238;
  color: red;
  display: flex;
  flex-wrap: wrap;
  border: 1px solid red;
}

.username {
  border: 1px solid red;
  width: 100%;
  margin: 10px 0px;
  height: 50px;
  display: flex;
  align-items: center;

}

.right {
  width: 75%;
  height: 550px;
  background: #eeeeee;
  display: flex;

  align-items: center;
  flex-direction: column;
}

.box {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
