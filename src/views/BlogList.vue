<template>
    <div>
        <h1>Blogul Mi Amor #1 Attempt</h1>
        <div v-if="blogList.length > 0">

            <BlogItem v-for="blog in blogList" :key="blog.id" :id="blog.id" :user="blog.user" :post="blog.post"
                :likes="blog.likes" :tag="blog.tag" 
                @like="likehandler($event)" 
                @dislike="dislikehandler($event)" />

        </div>
        <div v-else>
            <p>nici un post nu a fost creat</p>
        </div>
        <div>
            <input v-model="user" />
            <textarea v-model="post"></textarea>
            <select v-model="tag">
                <option value="general">general</option>
                <option value="flame">flame</option>
                <option value="recomandation">recomandation</option>

            </select>
            <button @click="submitformhandler">save</button>

        </div>
    </div>
</template>

<script>
import BlogItem from '@/components/BlogItem.vue';
import { myaxios } from '@/axios';
export default {
    components: {
        BlogItem,
    },
    data() {
        return {
            user: "",
            post: "",
            tag: "",
            blogList: []
        }
    },
    methods: {
        submitformhandler(event) {
            const newBlog = {
                user: this.user,
                post: this.post,
                tag: this.tag,

            }

            myaxios.post("/blog", newBlog).then((response) => {
                this.blogList = response.data.blogs
                console.log(newBlog)
            })
        },
        fetchBlogPosts() {
            myaxios.get("/blog").then(
                (response) => {
                    console.log(response.data.blogs)
                    this.blogList = response.data.blogs
                }
            )
        },
        likehandler(event) {
            console.log(event.itemId)
            myaxios.post('/blog/{$event.itemId}/like').then(
                (response) => {
                console.log(response.data.blogs),
                this.blogList = response.data.blogs
            }
            )
        },
        dislikehandler(event) {
            console.log(event.itemId)
        }
    },
    mounted(){
        this.fetchBlogPosts();
    }

}
</script>

<style lang="scss" scoped></style>