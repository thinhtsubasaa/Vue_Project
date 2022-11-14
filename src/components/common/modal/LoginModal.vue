<template>
    <div>
        <b-modal id="modal-1" title="BootstrapVue" v-model="showLogin" @hidden="callOnHide" @ok="handleOk"
            :ok-disabled="isDisableOk" :no-close-on-backdrop="true">
            <form>
                <div class=" mb-3">
                    <label class="form-label">Email address</label>
                    <input type="email" class="form-control" v-model="email">
                </div>
                <div class="mb-3" v-if="isRegisterModal">
                    <label class="form-label">Name</label>
                    <input type="text" class="form-control" v-model="userName">
                </div>
                <div class="mb-3">
                    <label class="form-label">Password</label>
                    <input type="password" class="form-control" v-model="password">
                </div>
            </form>
        </b-modal>
    </div>
</template>
<script>
// import Vue from "vue";
export default {
    name: 'LoginModal',
    data() {
        return {
            userName: '',
            showLogin: false,
            inValid: false,
            email: '',
            password: '',
            userInfo: {},
            reset: true,
            isDisableOk: true
        }
    },
    props: {
        isShowLogin: {
            type: Boolean,
            default: false
        },
        callGetUserInfo: {
            type: Function,
            default: () => { }
        },
        isRegisterModal: {
            type: Boolean,
            default: false
        },
        callOnHide: {
            type: Function,
            default: () => { }
        },

    },
    mounted() {

    },
    watch: {
        userName(value) {
            this.userInfo.userName = value;
        },
        email(value) {
            this.userInfo.email = value;
            if (value.length < 10) {
                this.isDisableOk = true
            } else {
                this.isDisableOk = false
            }
            // this.$emit('someEvent', this.userInfo)
            // this.userInfo.email = value
            // this.callGetUserInfo(this.userInfo)
        },
        password(value) {
            this.userInfo.password = value
            // this.$emit('someEvent', this.userInfo)
            // this.userInfo.password = value
            // this.callGetUserInfo(this.userInfo)
        },
        isShowLogin(value) {
            console.log("loginModal: ", value)
            this.showLogin = value
            if (this.isRegisterModal) {
                // Vue.nextTick(function () {

                // })
                this.userName = ''
                this.password = ''
            }
        },
        inValid(value) {
            this.reset = false
            if (value === true) {
                // ventBus.$emit('hello', 'i hear you');

            }
            this.reset = true
        },


    },
    methods: {
        handleOk() {
            this.$emit('someEvent', this.userInfo)
        },
    }
}
</script>