<template>
    <div>
      <h5>{{ user }}</h5>
      <p>{{ post }}</p>
      <div>
           <button @click="likeItem">like</button>
           <button>{{ likes }}</button>
           <button @click="dislikeItem">dislike</button>
           <button>{{ dislike }}</button>
      </div>
    </div>
    
</template>

<script>
    export default {
        props: {
            id: Number,
            user: String,
            post: String,
            likes: Number,
            tag: String
        },
        emits:['like','dislike'],
        methods: {
            likeItem() {
                this.$emit("like", {itemId: this.id})
            },
            dislikeItem() {
                this.$emit("dislike", {itemId:this.id})
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>
