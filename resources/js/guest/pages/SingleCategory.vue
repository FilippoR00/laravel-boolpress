<template>
    <div class="container">
        <h2>{{category.name}}</h2>
        <h3>Lista post associati:</h3>
        <ul v-if="category.post && category.post.length">
            <li v-for="post in category.post" :key="post.id"><router-link :to="{name: 'single-post', params: {slug: post.slug, title: post.title}}">{{post.title}}</router-link></li>
        </ul>
        <p v-else>Non sono presenti post associati a questa categoria.</p>
    </div>
</template>

<script>
export default {
    name: "SingleCategory",
    data() {
        return {
            category: []
        }
    },
    created() {
        axios.get(`/api/categories/${this.$route.params.slug}`)
            .then( (response) => {
                this.category = response.data;
            }).catch( (error)=> {
                this.$router.push({name: 'page-404'})
            })
    },
}
</script>

<style scoped lang="scss">
    h2{
        margin: 50px 25px;
    }
    h3{
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
    p{
        margin: 25px;
    }
</style>