<template>
	<div>
		<div v-if="loading" class="loading-indicator">Загрузка...</div>
		<ul class="chat-list">
			<message-item v-for="message in messagesWithId" :message="message.text" :key="message.id" />
		</ul>
	</div>
</template>

<script>
import MessageItem from '@/components/MessageItem'
import { v4 as uuidv4 } from 'uuid';
export default {
	components: {
		MessageItem
	},
	props: {
		messages: {
			type: Array,
			required: true
		},
		loading: {
			type: Boolean,
			required: true
		}
	},
	computed: {
		messagesWithId() {
			if (this.messages && this.messages.result) {
				return this.messages.result.map((message) => {
					return {
						id: uuidv4(),
						text: message,
					};
				});
			} else {
				return [];
			}
		},
	},
}
</script>
<style scoped>
.chat-list {
	display: flex;
	flex-direction: column;
	border-bottom: 1px solid #ccc;
	margin: 0;
	padding: 10px;
	padding-bottom: 60px;
}

.loading-indicator {
	text-align: center;
	color: #888;
}
</style>