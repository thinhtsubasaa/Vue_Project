<template>
    <div>
        <b-toast id="my-toast" variant="warning" solid >
            <template #toast-title>
                <div class="d-flex flex-grow-1 align-items-baseline">
                    <b-img blank blank-color="#ff5555" class="mr-2" width="12" height="12"></b-img>
                    <strong class="mr-auto">Notice!</strong>
                    <small class="text-muted mr-2">42 seconds ago</small>
                </div>
            </template>
            This is the content of the toast.
            It is short and to the point.
        </b-toast>
    </div>
</template>
<script>
export default {
    name: 'CustomToast',
    methods: {
        showToast() {
            console.log('showToast')
            this.$bvToast.toast('my-toast',{
                title: 'BootstrapVue Toast',
                autoHideDelay: 100000,
                noAutoHide: true 
                
            });
        }
    }
}
</script>