<template>
    <div :style="config"></div>
</template>

<script>
export default {
    name: 'highlight',
    props: {
        background: {
            default: 'rgba(33, 34, 50, 0.8)'
        },
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
        this.initHighlight()
        window.onresize = this.initHighlight
    },
    destroyed () {
        for (let i = 0; i < this.targets.length; i++) {
            this.targets[i].style['pointer-events'] = this.pointBackup[i]
            this.targets[i].classList.remove('highlight')
        }
    },
    methods: {
        initHighlight () {
            this.targets = document.querySelectorAll(this.selectors)
            for (let target of this.targets) {
                let client = target.getBoundingClientRect()
                target.style['z-index'] = '1001'
                target.style['position'] = 'relative'
                target.style['height'] = `${client.height}px`
                target.style['width'] = `${client.width}px`
                if (!target.classList.contains('highlight')) {
                    target.classList.add('highlight')
                }
                if (!this.event) {
                    this.pointBackup.push(target.style['pointer-events'])
                    target.style['pointer-events'] = 'none'
                }
            }
        }
    }
}
</script>

<style scpoed>
.highlight {
    outline: 1px dashed #ffffff;
    border: 2px solid #4a4b58;
}
</style>
