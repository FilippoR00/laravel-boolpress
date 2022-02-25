<template>
    <div class="container">
        <div class="center">
            <h1>Errore 404 :(</h1>
            <h2>Pagina non trovata!!!</h2>
        </div>
    </div>
</template>

<script>
export default {
    name: "PageNotFound"
}
</script>

<style scoped lang="scss">
    .center{
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        text-align: center;
        h1{
            font-size: 50px;
            margin-bottom: 15px;
        }
    }
</style>