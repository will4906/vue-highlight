<template>
    <canvas id="h-canvas">
        当前浏览器不支持canvas
    </canvas>
</template>

<script>
export default {
    name: 'highlight',
    props: {
        background: {
            default: 'rgba(33, 34, 50, 0.8)'
        },
        zIndex: {
            default: '1000'
        },
        selector: {
            required: true
        }
    },
    data () {
        return {}
    },
    mounted () {
        this.initCanvas()
    },
    methods: {
        initCanvas () {
            let hCanvas = document.getElementById('h-canvas')
            hCanvas.getContext
            // console.log('init')
        }
    }
}
</script>

<style>

</style>
