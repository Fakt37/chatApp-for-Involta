<template>
	<div id="chatContainer" class="chat-container" @scroll="checkScroll">
		<message-list :messages="messages" :loading="loading" />
		<message-form @create="createMessage" />
	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';
import MessageList from '@/components/MessageList.vue';
import MessageForm from '@/components/MessageForm.vue';

interface MyData {
	messages: {
		result: string[];
	};
	offset: number;
	loading: boolean;
}

export default defineComponent({
	components: {
		MessageList,
		MessageForm,
	},
	data(): MyData {
		return {
			messages: { result: [] },
			offset: 0,
			loading: false,
		};
	},
	methods: {
		createMessage(newMessage: string) {
			this.messages.result.push(newMessage);
		},
		async fetchMessages() {
			this.loading = true;
			try {
				const res = await axios.get(`https://numia.ru/api/getMessages?offset=${this.offset}`);
				if (res.data.result) {
					this.messages.result = [...res.data.result.reverse(), ...this.messages.result];
				} else {
					console.error(res.data);
				}
			} catch (e) {
				console.error('Ошибка:', e);
			} finally {
				this.loading = false;
			}
		},
		checkScroll() {
			const chatContainer = document.getElementById('chatContainer');
			if (chatContainer && chatContainer.scrollTop === 0 && !this.loading) {
				this.offset += 20;
				this.fetchMessages();
			}
		}
	},
	mounted() {
		this.fetchMessages();
	}
});
</script>

<style>
* {
	margin: 0;
	font-family: 'Arial', sans-serif;
	box-sizing: border-box;
}

#app {
	display: flex;
	flex-direction: column;
	height: 100vh;
	padding: 10px;
}

.chat-container {
	height: 100%;
	overflow-y: auto;
}
</style>
