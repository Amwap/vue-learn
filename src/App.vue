<template>
 <div class="app">
	<h1>Posts</h1>
	<div class="app__btns">
		<Button @click='fetchPosts'>Update posts</Button>
		<Button @click='showDialog'>Create post</Button>
		<Select v-model="selectedSort" :options="sortOptions"/>
	</div>
	
	<Dialog v-model:show='dialogVisible'>
		<!-- @create = прослушивание и привязка событий к функции -->
		<PostForm @create="createPost" />
	</Dialog>
	<PostList :posts="sortedPosts" @remove="removePost" v-if="!postsLoading"/>
	<!-- <PostList :posts="posts" @remove="removePost" v-if="!postsLoading"/> sortedPosts возвращает отсортированный массив -->
	<div class='loading' v-else>loading...</div>
 </div>
</template>

<script>
import PostForm from './components/PostForm.vue'; // можно с точкой
import PostList from '@/components/PostList.vue'; // можно без
import axios from 'axios';

export default {
	components: {
		// импорт компонентов
		PostForm, PostList
	},
	data(){
		return{
			// модели
			posts: [
				// {id: 1, title: 'title 1', body: 'descr 1'},
				// {id: 2, title: 'title 2', body: 'descr 2'},
				// {id: 3, title: 'title 3', body: 'descr 3'}
			],
			dialogVisible: false,
			postsLoading: false,
			selectedSort: '',
			sortOptions:[
				{value: 'title', name: 'By name'},
				{value: 'body', name: 'By body'},
			]
		}
	},
	methods: {
		// методы
		createPost(post){
			// создание поста из формы диалога
			this.posts.push(post)
			this.dialogVisible = false;
		},
		removePost(post){
			// удаляет пост по нажатию на кнопку delete
			this.posts = this.posts.filter(p => p.id !== post.id)
		},
		showDialog(){
			// отображение диалога по нажатию на кнопку create post
			this.dialogVisible = true;
		},
		async fetchPosts(){
			// получает данные с сервера
			try {
				setTimeout(async () => {
					this.postsLoading = true
					const responce = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
					this.posts = responce.data
					this.postsLoading = false
			 	}, 1000);
			} catch (e) {
				alert(e)
			} finally{
				this.postsLoading = false
			}
		},
	},
	mounted() { 
		// хуки https://v3.ru.vuejs.org/ru/guide/instance.html#%D0%B4%D0%B8%D0%B0%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B0-%D0%B6%D0%B8%D0%B7%D0%BD%D0%B5%D0%BD%D0%BD%D0%BE%D0%B3%D0%BE-%D1%86%D0%B8%D0%BA%D0%BB%D0%B0
		// отрабатывает при загрузке текущего компонента
		this.fetchPosts()
	},
	computed:{
		sortedPosts(){
			return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
		}
	},
	watch:{ // отслеживает изменения в моделях
		selectedSort(newValue) {
			// // отрабатывает при изменении модели. 
			// // принимает новое значение, должна иметь название модели
			// this.posts.sort((post1, post2) => {
			// 	return post1[newValue]?.localeCompare(post2[newValue])
			// })
			// console.log(newValue)
		},
		dialogVisible(newValue) {
			// отрабатывает при изменении модели. 
			// принимает новое значение, должна иметь название модели
			console.log(newValue)
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

.app__btns{
	margin: 15px;
	justify-content: space-between;
	display: flex;
}
</style>