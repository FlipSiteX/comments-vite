<template>
	<Comment
		v-for="comment in comments"
		:key="comment.id"
		:comment
		@remove="(id) => $emit('remove', id)"
	/>
</template>

<script>
import Comment from "./Comment.vue";
export default {
	components: {
		Comment,
	},
	props: {
		comments: {
			type: Array,
			required: true,
		},
	},
};
</script>

<style></style>
