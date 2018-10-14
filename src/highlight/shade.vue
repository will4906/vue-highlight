<template>
    <div class="shade"></div>
</template>

<script>
export default {
    name: 'shade',
    props: {
        shadeTheme: {
            default: 'black'
        }
    }
}
</script>

<style lang="scss" scpoed>
.shade {
    position: relative;
}
</style>
