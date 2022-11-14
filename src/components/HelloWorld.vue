<template>
  <div class="hello">

    <button style="margin-left:50%" v-if="showLoginBtn" @click="showLogin">Login</button>
    <button style="margin-left:50%" v-else @click="logout">Logout</button>
    <LoginModal :isShowLogin="isShowLogin" @someEvent="catchEmit" :callGetUserInfo="getUserInfo"
      :callOnHide="onErrorModalHiden" :isRegisterModal="isShowRegister" />
    <WelcomeModal :giatriCuaError="giatriCuaError" />
    <ErrorModal :isshowError="showError" :callOnHide="onErrorModalHide" :callHandleOk="openRegister" />
    <ArGrid v-if="!showLoginBtn" :isShowAgGird="isShowAgGird" :callOnHide="onErrorModalHidenn" />
    <button @click="showToast">Show Toast</button>
    <Toast :isshowToastFirst="showToastFirst" :isshowToastSecond="showToastSecond"/>
    <CustomToast ref="customToast"/>
  </div>
</template>

<script>
import LoginModal from './common/modal/LoginModal.vue'
import WelcomeModal from './common/modal/WelcomeModal.vue'
import ErrorModal from './common/modal/ErrorModal.vue'
import Toast from './common/modal/Toast.vue'
import ArGrid from './Grid/AgGrid.vue'
import CustomToast from './common/CustomToast.vue'
export default {
  name: 'HelloWorld',
  components: { LoginModal, WelcomeModal, ErrorModal, ArGrid, Toast, CustomToast},

  data() {
    return {
      isShowRegister: false,
      userName: '',
      isShowLogin: false,
      showError: false,
      showToastFirst:false,
      showToastSecond:false,
      giatriCuaLogin: {},
      giatriCuaError: {},
      userInfo: {
        email: "",
        password: ""
      },
      showLoginBtn: true,
      isShowAgGird: false,
      registeredUser: {
        email: 'abc@fsoft.com',
        password: '123456'
      },
      errorTimes: 0
    }
  },
  watch: {
    giatriCuaLogin(value) {
      console.log('isShowLogin: ', value)
      this.giatriCuaError = { a: 'aaa' }
    }
  },
  methods: {
    showToast() {
      this.$refs.customToast.showToast()
      console.log('showToast')
    },
    openRegister() {
      this.isShowRegister = true
      this.isShowLogin = true
    },
    logout() {
      this.showLoginBtn = true
    },


    showLogin() {
      console.log('showLogin')
      this.isShowLogin = !this.isShowLogin
      // this.showLoginBtn = false
    },

    catchEmit(value) {
      console.log('cacth emit')
      if (value.email === this.registeredUser.email && value.password === this.registeredUser.password) {
        this.showLoginBtn = false
        this.errorTimes = 0
        this.showToastFirst = true
          
      } else {
        this.showToastSecond = true
        if (this.errorTimes >= 1) {

          this.showError = true
          this.isShowLogin = false
        }
        this.errorTimes += 1
      }
    },
    getUserInfo(userInfo) {
      this.userInfo = userInfo;
      console.log('user:', userInfo);

    },
    onErrorModalHide() {
      console.log('onHide');
      this.showError = false;
      this.errorTimes = 0;
    },
    onErrorModalHiden() {
      console.log('onHidden')
      this.isShowLogin = false;
      if (this.isShowRegister === true) {
        this.isShowRegister = false
      }
    },
    onErrorModalHidenn() {
      console.log('onHiddenn')
      this.isShowAgGird = false;
    },

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
