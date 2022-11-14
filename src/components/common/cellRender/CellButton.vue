<template>
    <div>
        <button @click="onClick">{{text}}</button>
    </div>
</template>
<script>
export default {
    name: 'CellButton',
    props: {
        text: {
            type: String,
            default: 'Button'
        }
    },
    mounted() {
        console.log('render cell button')
    },
    methods: {
        onClick() {
            this.params.onBtnClick(this.params.data)
        }
    }
}
</script>