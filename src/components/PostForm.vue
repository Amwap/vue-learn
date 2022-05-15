<template>
	
    <form action="" @submit.prevent>
        <h1>Create post</h1>
        <Input 
			v-model='post.title'
            type="text" 
            placeholder="Title"
        />
        <Input 
			v-bind:value="post.description"
			@input="post.description = $event.target.value"
            type="text" 
            placeholder="Description"
        />
        <Button  @click="createPost">POST</Button>
    </form>
</template>

<script>
export default {
	data(){
		return{
			post:{
				title: '',
				description: '',
			}
		}
	},
	methods: {
		createPost(){
			this.post.id = Date.now(),
			this.$emit('create', this.post)
			this.post = {
				title: '',
				description: '',
			}
		},
	}
}

</script>

<style scoped>
form{
	display: flex;
	flex-direction: column;
	align-items: center;
}


</style>