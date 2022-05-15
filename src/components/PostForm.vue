<template>
    <form action="" @submit.prevent>
        <h1>Create post</h1>
        <Input 
			v-model.trim='post.title'
			type="text" 
			placeholder="Title" 
		/> <!-- двухстороннее связывание через v-model  -->
		
        <Input 
			v-bind:value="post.body" 
			@input="post.body = $event.target.value" 
			type="text"  
			placeholder="Body" 
		/> <!-- двухстороннее связывание через v-bind. хз почему работает, но работает  -->
        <Button  
			@click="createPost"
		>POST</Button>
    </form>
</template>

<script>
export default {
	data(){
		return{
			post:{
				title: '',
				body: '',
			}
		}
	},
	methods: {
		createPost(){
			this.post.id = Date.now(),
			this.$emit('create', this.post) // Триггер события внутри компонента
			this.post = {
				title: '',
				body: '',
			}
		},
	}, 
	watch:{
		post: {
			// Глубокое отслеживание объекта для моделей компонентов
			handler(newValue){
				// console.log(newValue)
			},
			deep: true
		}
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