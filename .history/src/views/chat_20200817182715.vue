<template>
  <div class="box">
    <div class="container">
      <div class="left"></div>
      <div class="right">
        <div class="top">聊天室()</div>
        <div class="line"></div>
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
      userLists: [],
    };
  },
  methods: {
    getData() {
      this.sockets.subscribe("relogin", (data) => {
        console.log(data);
      });
    },
    send() {
      this.$socket.emit("sendMessage", this.value);
    },
  },
  mounted() {
    this.getData();
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
.line{
  width: 80%;
  background: gray;
}
.top{
  display: flex;
  justify-content: center;
  align-items: center;
  height: 60px;
 
}
.container{
  display: flex;
  width: 60%;
  height: 550px;
 
}

.left{
  width: 20%;
  height: 550px;
  background: #2E3238;
}
.right{
  width: 80%;
  height: 550px;
  background: #EEEEEE;
}
.box {

  display: flex;
  align-items: center;
  justify-content: center;

}

</style>
