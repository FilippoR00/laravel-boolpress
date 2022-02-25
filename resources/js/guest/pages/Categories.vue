<template>
    <div class="container">
        <h2>Categorie:</h2>
        <ul>
            <li v-for="category in categories" :key="category.id">
                <router-link :to="{name: 'single-category', params: {slug: category.slug}}">{{category.name}}</router-link>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "categories",
    data() {
        return {
            categories: []
        }
    },
    created() {
        axios.get(`/api/categories`)
            .then( (response) => {
                this.categories = response.data;
            });
    },
}
</script>

<style scoped lang="scss">
    h2{
        margin: 50px 25px;
    }
    ul{
        margin: 50px 25px;
        li{
            list-style: none;
            margin: 10px 0px;
            a{
                padding: 5px 0px;
                color: black;
                text-decoration: none;
                font-size: 20px;
                transition: 0.15s all;
            }
            a:hover{
                color: #5e5eff;
                border-bottom: 3px solid #5e5eff;
            }
        }
    }
</style>