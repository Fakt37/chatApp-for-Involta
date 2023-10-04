<template>
	<li class="message">{{ message }}</li>
</template>
<script>
export default {
	props: {
		message: {
			type: String,
			required: true
		}
	}
}
</script>
<style scoped>
.message {
	width: 500px;
	align-self: end;
	background-color: #f0f0f0;
	margin-top: 10px;
	padding: 10px;
	border-radius: 5px;
	list-style: none;
	text-align: right;
	word-wrap: break-word;
	white-space: pre-wrap;
}
</style>