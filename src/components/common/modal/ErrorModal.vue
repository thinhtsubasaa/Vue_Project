<template>
    <div>
        <b-modal id="modal-1" title="BootstrapVue" v-model="showError" @hidden="callOnHide" @ok="callHandleOk">
            <p>Email {{ userName }} Khong ton tai</p>
            <p>Ban co muon tao tai khoan moi khong</p>
        </b-modal>
    </div>
</template>
<script>
export default {
    name: 'ErrorModal',
    data() {
        return {
            showError: false
        }
    },
    watch: {
        isshowError(value) {
            this.showError = value
        }
    },
    created() {

    },
    props: {
        userName: String,
        isshowError: {
            type: Boolean,
            default: false

        },
        callOnHide: {
            type: Function,
            default: () => { }
        },
        callHandleOk: {
            type: Function,
            default: () => { }
        }
    },
    methods: {
    }

}


</script>
