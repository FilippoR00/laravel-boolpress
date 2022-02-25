<template>
    <header>
        <div class="container">
            <div class="left">
                <router-link class="logo" :to="{name: 'home'}">Boolpress</router-link>
                <ul>
                    <li><router-link :to="{name: 'home'}">Home</router-link></li>
                    <li><router-link :to="{name: 'about'}">Chi siamo</router-link></li>
                    <li><router-link :to="{name: 'categories'}">Categorie</router-link></li>
                </ul>
            </div>
            <div class="right">
                <a href="/admin/home">Area riservata</a>
            </div>
        </div>
    </header>
</template>

<script>
export default {
    name: "Header",
}
</script>

<style lang="scss" scoped>
    header{
        background-color: #3535ec;
        height: 100px;
        color: 	white;
        position: sticky;
        top: 0;
        .container{
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 100%;
            .left{
                width: 80%;
                display: flex;
                align-items: center;
                .logo{
                    color: white;
                    text-decoration: none;
                    font-size: 40px;
                    
                }
                ul{
                    margin-left: 30px;
                    display: flex;
                    li{
                        list-style: none;
                        a{
                            color: white;
                            text-decoration: none;
                            padding: 10px 20px;
                            transition: 0.3s all;
                            border: 1px solid #4d4dff;
                        }
                        a:hover{
                            background-color: #4d4dff;
                        }
                        .router-link-exact-active{
                            background-color: #5e5eff;
                        }
                    }
                            li:first-child a{
                                border-start-start-radius: 20px;
                                border-end-start-radius: 20px;
                            }
                            li:last-child a{
                                border-start-end-radius: 20px;
                                border-end-end-radius: 20px;
                            }
                }
            }
            .right{
                width: 20%;
                a{
                    background-color: #5e5eff;
                    padding: 15px 25px;
                    border-radius: 10px;
                    color: white;
                    text-decoration: none;
                    transition: 0.3s all;
                }
                a:hover{
                    background-color: #6d6dff;
                }
            }
        }
    }
</style>