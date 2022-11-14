<template>
    <div>
        <button @click="onClick">{{text}}</button>
    </div>
</template>
<script>
export default {
    name: 'CellEdit',
    props: {
        text: {
            type: String,
            default: 'Button'
        }
    },
    mounted() {
        console.log('render cell edit button')
    },
    methods: {
        onClick() {
            this.params.onBtnClick(this.params.data)
        }
    }
}
</script>