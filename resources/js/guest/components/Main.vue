<template>
    <main>
        <router-view></router-view>
    </main>
</template>

<script>
export default {
    name: "Main",
    // mounted() {
    //     document.title = this.$route.meta.title;
    // },
}
</script>

<style lang="scss" scoped>
    main{
        min-height: 100vh;
    }
</style>