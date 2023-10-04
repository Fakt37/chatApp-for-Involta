<template >
	<button>
		<slot></slot>
	</button>
</template>
<script>
export default {
	name: 'my-button'
}
</script>
<style scoped>
button {
	padding: 8px 16px;
	background-color: #4caf50;
	color: #fff;
	border: none;
	border-radius: 5px;
	cursor: pointer;
}

button:hover {
	background-color: #45a049;
}
</style>