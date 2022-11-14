<template>

    <div>

        <b-toast  variant="success" auto-hide-delay="5000" solid v-model="showToastFirst" no-auto-hide>
            <template #toast-title>
                <div class="d-flex flex-grow-1 align-items-baseline">
                    <b-img blank blank-color="#ff5555" class="mr-2" width="12" height="12"></b-img>
                    <strong class="mr-auto">Notice!</strong>
                    <small class="text-muted mr-2">42 seconds ago</small>
                </div>
            </template>
            DANG NHAP THANH CONG
        </b-toast>

        <b-toast  variant="warning" auto-hide-delay="15000" solid v-model="showToastSecond" :no-auto-hide="true">
            <template #toast-title>
                <div class="d-flex flex-grow-1 align-items-baseline" >
                    <b-img blank blank-color="#ff5555" class="mr-2" width="12" height="12"></b-img>
                    <strong class="mr-auto">Notice!</strong>
                    <small class="text-muted mr-2">42 seconds ago</small>
                </div>
            </template>
            DANG NHAP THAT BAI
        </b-toast>
    </div>

</template>

<script>
export default {
    // eslint-disable-next-line
    name: 'Toast',
    data() {
        return {
            showToastFirst: false,
            showToastSecond: false,

        }
    },
    watch: {
        isshowToastFirst(value) {
            this.showToastFirst = value
        },
        isshowToastSecond(value) {
            console.log('isshowToastSecond: ', value)
            this.showToastSecond = value
        }
    },
    created() {

    },
    props: {

        isshowToastFirst: {
            type: Boolean,
            default: false

        },
        isshowToastSecond: {
            type: Boolean,
            default: false

        }
    },
    methods: {

    },
}
</script>

<style>

</style>