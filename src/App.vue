<template>
 <div class="app">
	<h1>Posts</h1>
	<Button 
		@click='showDialog'
		style='margin:15px'
	>Создать пост</Button>
	<Dialog v-model:show='dialogVisible'>
		<PostForm @create="createPost" />
	</Dialog>
	<PostList 
		:posts="posts" 
		@remove="removePost"
	/>
 </div>
</template>

<script>
import PostForm from '@/components/PostForm.vue'
import PostList from '@/components/PostList.vue'

export default {
	components: {
		PostForm, PostList
	},
	data(){
		return{
			posts: [
				{id: 1, title: 'title 1', description: 'descr 1'},
				{id: 2, title: 'title 2', description: 'descr 2'},
				{id: 3, title: 'title 3', description: 'descr 3'}
			],
			dialogVisible: false,
		}
	},
	methods: {
		createPost(post){
			this.posts.push(post)
			this.dialogVisible = false;
		},
		removePost(post){
			this.posts = this.posts.filter(p => p.id !== post.id)
		},
		showDialog(){
			this.dialogVisible = true;
		}
	}
}
</script>

<style>
*{
   margin: 0;
   padding: 0;
   box-sizing: border-box;
}
.app{
  padding: 20px;
}
</style>