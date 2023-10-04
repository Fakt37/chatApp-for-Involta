<template>
	<input type="text" :value="modelValue" @input="updateInput">
	<!-- //Можно было бы использовать props но в данном случае хватит text -->
</template>
<script>
export default {
	name: 'my-input',
	props: {
		modelValue: [String]
	},
	methods: {
		updateInput(e) {
			this.$emit('update:modelValue', e.target.value)
		}
	}
}
</script>
<style scoped>
input {
	flex: 1;
	padding: 8px;
	margin-right: 10px;
	border: 1px solid #ccc;
	border-radius: 5px;
}
</style>