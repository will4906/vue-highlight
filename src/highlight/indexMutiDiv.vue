<template>
    <div class="container" :style="containerStyle">
        <div class="top" :style="topStyle"></div>
        <div class="middle" :style="middleStyle">
            <div class="left" :style="leftStyle"></div>
            <div class="main" :style="mainStyle"></div>
            <div class="right" :style="rightStyle"></div>
        </div>
        <div class="bottom" :style="bottomStyle"></div>
    </div>
</template>

<script>
import Vue from 'vue'
/* eslint-disable */
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
        return {
            containerStyle: {
                'z-index': this.zIndex
            },
            topStyle: {
                background: this.background,
                width: '100%'
            },
            middleStyle: {
                display: 'flex'
            },
            leftStyle: {
                background: this.background,
                left: '0'
            },
            mainStyle: {
                'z-index': 1001,
                border: '2px solid #4a4b58',
                outline: '1px dashed #ffffff'
            },
            rightStyle: {
                background: this.background,
                'z-index': 1000,
                right: 0,
                flex: 1
            },
            bottomStyle: {
                background: this.background,
                width: '100%',
                height: '100%',
                bottom: 0
            }
        }
    },
    mounted () {
        this.initAllStyle()
        window.onresize = this.initAllStyle
    },
    methods: {
        getTargetClient () {
            let target = document.querySelector(this.selector)
            if (target) {
                return target.getBoundingClientRect()
            } else {
                return null
            }
        },
        // 初始化上div样式
        initTopStyle () {
            let client = this.getTargetClient()
            if (client) {
                Vue.set(this.topStyle, 'height', `${client.y}px`)
            }
        },
        // 初始化中间行
        initMiddleStyle () {
            let client = this.getTargetClient()
            if (client) {
                Vue.set(this.middleStyle, 'height', `${client.height}px`)
            }
        },
        // 初始化左div样式
        initLeftStyle () {
            let client = this.getTargetClient()
            if (client) {
                Vue.set(this.leftStyle, 'height', `${client.height}px`)
                Vue.set(this.leftStyle, 'width', `${client.x}px`)
            }
        },
        // 初始化高亮目标位置样式
        initMainStyle () {
            let client = this.getTargetClient()
            if (client) {
                Vue.set(this.mainStyle, 'height', `${client.height}px`)
                Vue.set(this.mainStyle, 'width', `${client.width}px`)
            }
        },
        // 初始化右div样式
        initRightStyle () {
            let client = this.getTargetClient()
            if (client) {
                Vue.set(this.rightStyle, 'height', `${client.height}px`)
            }
        },
        // 初始化底部div样式
        initBottomStyle () {
            let client = this.getTargetClient()
            if (client) {
                Vue.set(this.bottomStyle, 'top', `${client.height + client.y}px`)
            }
        },
        /**
         * 初始化全部样式，如外部元素有更新则需要调用此函数刷新当前布局
         */
        initAllStyle () {
            this.initTopStyle()
            this.initMiddleStyle()
            this.initLeftStyle()
            this.initMainStyle()
            this.initRightStyle()
            this.initBottomStyle()
        }
    }
}
</script>

<style scoped>
.container {
    position: fixed;
    text-align: left;
    width: 100%;
    height: 100%;
}
</style>
