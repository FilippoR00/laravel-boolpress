<template>
    <div class="container">
        <h2>{{post.title}}</h2>
        <img v-if="post.image" :src="`/storage/${post.image}`" :alt="post.title + ' image' ">
        <p>{{post.content}}</p>
        <div v-if="post.category" class="category">
            Categoria: {{post.category.name}}
        </div>
        <div v-if="post.tags" class="tags">
            <span>Tag:</span>
            <ul>
                <li v-for="tag in post.tags" :key="tag.id">
                    {{tag.name}}
                </li>
            </ul>
        </div>
        <h3>Inserisci commento:</h3>
        <form @submit.prevent="addComment">
            <div>
                <input type="text" id="name" placeholder="Inserisici il nome" v-model="formData.name">
            </div>
            <div>
                <textarea name="content" id="content" cols="30" rows="8" placeholder="Inserisci il commento" v-model="formData.content"></textarea>
                <div v-if="formErrors.content">
                    <ul>
                        <li class="error" v-for="(error, index) in formErrors.content" :key="index">
                            {{error}}
                        </li>
                    </ul> 
                </div>
            </div>
            <div>
                <button type="submit">Invia</button>
            </div>
        </form>
        <div v-show="commentSent" class="approvation">
            Commento in fase di approvazione...
        </div>
        <div v-show="comments.length > 0">
            <h3>Commenti:</h3>
            <div class="comment" v-for="comment in comments" :key="comment.id">
                <div class="name">
                    {{comment.name}}
                </div> 
                <div class="content">
                    {{comment.content}}
                </div> 
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "SinglePost",
    data() {
        return {
            post: [],
            comments: [],
            formData: {
                name: '',
                content: '',
                post_id: null,
            },
            commentSent: false,
            formErrors: [],
        }
    },
    methods: {
        addComment(){
            axios.post(`/api/comments`,this.formData)
            .then( (response) => {
                this.formData.name = "";
                this.formData.content = "";
                this.commentSent = true;
            }).catch( (error)=> {
                this.formErrors = error.response.data.errors;
            })
        }
    },
    created() {
        axios.get(`/api/posts/${this.$route.params.slug}`)
            .then( (response) => {
                this.post = response.data;
                this.formData.post_id = this.post.id;
            }).catch( (error)=> {
                this.$router.push({name: 'page-404'})
            })
        axios.get(`/api/comments`)
            .then( (response) => {
                this.comments = response.data;
            })
    },
}
</script>

<style scoped lang="scss">
    h2{
        margin: 50px 25px;
    }
    h3{
        margin: 20px 0px;
    }
    form{
        background-color: #ddd;
        width: 100%;
        input{
            width: calc(100% - 20px);
            margin: 10px;
            border: 1px solid black;
            border-radius: 5px;
            padding: 10px 20px;
            font-size: 18px;
        }
        textarea{
            width: calc(100% - 20px);
            margin: 10px;
            border: 1px solid black;
            border-radius: 5px;
            padding: 10px 20px;
            font-size: 18px;
        }
        button{
            width: 100px;
            padding: 10px 20px;
            font-size: 18px;
            margin: 10px;
            color: white;
            background-color: #3535ec;
            transition: 0.2s all;
            border: 3px solid #3535ec;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover{
            background-color: #5e5eff;
        }
        .error{
            background-color: #f2645c;
            padding: 10px;
            margin: 5px 10px;
            border-radius: 10px;
            color: white;
            list-style: none;
        }
    }
    .approvation{
        background-color: #5e5eff;
        padding: 10px;
        color: white;
    }
    .comment{
        background-color: #ddd;
        width: 400px;
        margin: 20px;
        padding: 20px;
        border-radius: 25px;
        .name{
            font-weight: 600;
            margin-bottom: 10px;
        }
        .content{
    
        }
    }
</style>