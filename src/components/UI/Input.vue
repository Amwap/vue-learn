<template>
    <input :value="modelValue" @input="updateInput" class="input" type="text">
</template>

<script>
export default {
    name: "Input",
	props:{
		modelValue: [String, Number]
	},
	methods: {
		updateInput(event){
			this.$emit('update:modelValue', event.target.value) // Триггер события внутри компонента с привязкой к модели
		}
	}
}

</script>

<style>
.input{
	width: 100%;
	border: 1px solid teal;
	padding: 10px 15px;
	margin-top: 8px;
	margin-bottom: 8px;
}
</style>