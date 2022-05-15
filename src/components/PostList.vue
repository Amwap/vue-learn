<template>
    <h2> List of posts</h2>
    <div v-show='posts.length == 5'>
        <h2>Count of items more then 5</h2>
    </div>
    <div v-if='posts.length > 0'>
        <div>
            <PostItem  
                v-for="post in posts" 
                :post="post" 
                :key="post.id"
                @remove="$emit('remove', post)"
            />
        </div>
    </div>
    
    <div v-else class="empty-message">
        <h2>List is empty</h2>
    </div>
    
</template>


<script>
import PostItem from '@/components/PostItem.vue'

export default {
    components:{
        PostItem
    },
    props:{
        posts:{
            type: Array,
            required: true
        }
    }   
}
</script>


<style scoped>
.empty-message{
    color: red;
    width: 100%;
    text-align: center;
    justify-content: center;
    align-content: center;
}
</style>