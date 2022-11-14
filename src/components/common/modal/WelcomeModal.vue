<template>
    <div>
        <b-modal id="modal-1" title="BootstrapVue" v-model="showWelcome">
            <p>Chao {{ userName }}</p>
        </b-modal>
    </div>
</template>
<script>
export default {
    name: 'WelComeModal',
    data() {
        return {
            showWelcome: false
        }
    },
    watch: {
        isShowWelcome(value) {
            this.showWelcome = value
        }
    },
    
    props: {
            userName: String,
            isShowWelcome: {
                type: Boolean,
                default: false

            }
        }
    }
</script>
