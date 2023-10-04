<template>
	<form class="input-container" @submit.prevent>
		<my-input v-model="newMessage" placeholder="Введите сообщение..." />
		<my-button @click="sendMessage">Отправить</my-button>
	</form>
</template>
<script>
export default {
	data() {
		return {
			newMessage: ''
		}
	},
	methods: {
		sendMessage() {
			if (this.newMessage.trim() !== "") {
				this.$emit('create', this.newMessage)
				this.newMessage = "";
			}
		}
	}
}
</script>
<style scoped>
.input-container {
	position: fixed;
	right: 0;
	bottom: 0;
	left: 0;
	display: flex;
	height: 60px;
	padding: 10px;
	background-color: #fff;
}
</style>