<template>
  <div class="container">
    <div class="login" v-if="!flag">
      <div>用户登录</div>
      <div>
        username:
        <input type="text" v-model="value" />
      </div>
      <div>
        <div>选择头像</div>
        <div class="img-box">
          <div v-for="(item,index) in imgList" :key="index">
            <div class="pic" @click="addPic(item,index)" :class="num===index?'imgBorder':''">
              <img :src="item.name" alt />
            </div>
          </div>
        </div>
      </div>

      <div class="loginBtn" @click="loginBtn">登录</div>
    </div>
    <div v-if="flag">
          <div class="left">
      <div>
        <div class="username">
          <div class="avatar">
            <img :src="item.avatar" alt />
          </div>
          <div class="username-text">{{item.username}}</div>
        </div>
      </div>
      <div class="username" v-for="(item,index) in userlist" :key="index">
        <div class="avatar">
          <img :src="item.avatar" alt />
        </div>
        <div class="username-text">{{item.username}}</div>
      </div>
    </div>
    <div class="right">
      <div class="top">聊天室()</div>
      <div class="line"></div>

      <div class="content"></div>
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
      imgValue: "",
      num:'',
      imgList: [
        {
          name: require("../assets/avatar01.jpg"),
        },
        {
          name: require("../assets/avatar02.jpg"),
        },
        {
          name: require("../assets/avatar03.jpg"),
        },
        {
          name: require("../assets/avatar04.jpg"),
        },
        {
          name: require("../assets/avatar05.jpg"),
        },
        {
          name: require("../assets/avatar06.jpg"),
        },
        {
          name: require("../assets/avatar07.jpg"),
        },
        {
          name: require("../assets/avatar08.jpg"),
        },
        {
          name: require("../assets/avatar09.jpg"),
        },
        {
          name: require("../assets/avatar10.jpg"),
        },
      ],
      user: [],
      flag: false,
      listLeft:[],
    };
  },
  methods: {
    addPic(item,index) {
      this.imgValue = item.name;
      this.num = index
    },
    loginBtn() {
      console.log(this.$socket);
      this.flag = !this.flag
      this.$socket.emit("login", {
        username: this.value,
        avatar: this.imgValue,
      });
    },
  },
  sockets: {
    loginSuccess(data) {
      console.log("success", data);
    },
    loginError(data) {
      console.log(data);
    },
    userList(data) {
      this.listLeft = data
    },
  },
  mounted() {},
  watch: {},
  computed: {},
};
</script>

<style lang="scss" scoped>
.imgBorder{
  border: 2px solid red;
}
.img-box {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.pic {
  width: 70px;
  height: 60px;
}

img {
  width: 100%;
  height: 100%;
}

.container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.loginBtn {
  cursor: pointer;
  width: 200px;
  height: 40px;
  background: green;
  display: flex;
  align-items: center;
  justify-content: center;
}

.login {
  width: 400px;
  height: 500px;
  border: 1px solid gray;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.login div {
  margin-bottom: 20px;
}
</style>
