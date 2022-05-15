<template>
    <div class="post">
        <div>
            <div><strong>Title</strong> {{ post.title }} </div>
            <div><strong>Body</strong> {{ post.body }}</div>
        </div>
        <div class='post__btns'>
            <Button @click="$emit('remove', post)" >Delete</Button>
        </div>
   </div>
</template>

<script>
import Button from '@/components/UI/Button.vue'

export default {
	components:{
		Button
	},
    props:{
        post:{
            type: Object,
            required: true,
            
        }
    }
}
</script>

<style scoped>
.post{
    padding: 15px;
    border: 2px solid teal;
    margin-top: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>