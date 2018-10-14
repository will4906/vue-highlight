<template>
    <div :style="config"></div>
</template>

<script>
export default {
    name: 'highlight',
    props: {
        background: {
            default: 'red'
        },
        // 目标元素，这其实有点头大，不知道到底是应该给selector还是dom
        // 我们尝试两种方案，第一种放selector
        selectors: {
            required: true
        },
        event: {
            default: false
        }
    },
    computed: {
        config () {
            return {
                background: this.background,
                position: 'fixed',
                'z-index': 1000,
                height: '100%',
                width: '100%'
            }
        }
    },
    data () {
        return {
            targets: [],
            pointBackup: []
        }
    },
    mounted () {
        this.targets = document.querySelectorAll(this.selectors)
        for (let target of this.targets) {
            let client = target.getBoundingClientRect()
            target.style['z-index'] = '1001'
            target.style['position'] = 'relative'
            target.style['height'] = `${client.height}px`
            target.style['width'] = `${client.width}px`
            target.classList.add('highlight')
            if (!this.event) {
                this.pointBackup.push(target.style['pointer-events'])
                target.style['pointer-events'] = 'none'
            }
        }
    },
    destroyed () {
        for (let i = 0; i < this.targets.length; i++) {
            this.targets[i].style['pointer-events'] = this.pointBackup[i]
            this.targets[i].classList.remove('highlight')
        }
    }
}
</script>

<style lang="scss" scpoed>
.highlight {
    outline: 1px dashed #ffffff;
    border: 2px solid black;
}
</style>
