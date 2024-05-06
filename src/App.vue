<template>
	<section
		class="w-full rounded-lg border-2 border-purple-600 p-4 my-8 mx-auto max-w-3xl"
	>
		<div class="flex justify-between h-10 mb-3">
			<button
				class="bg-purple-600 hover:bg-purple-500 py-2 px-3 rounded text-white font-medium"
				@click="openDialog"
			>
				Добавить комментарий
			</button>
			<SortSelect
				:sortOptions
				v-model="selectedOption"
				class="mx-3"
			/>
			<SearchRow v-model="term" />
		</div>

		<h3 class="font-os text-lg font-bold">Комментарии</h3>
		<CommentsList
			:comments="searchComments"
			@remove="deleteComment"
		/>
	</section>
	<DialogWindow
		:showDialog
		@closeDialog="showDialog = false"
	>
		<CommentForm
			@addComment="addComment"
			@closeDialog="showDialog = false"
		/>
	</DialogWindow>
</template>

<script>
import CommentsList from "./components/CommentsList.vue";
import DialogWindow from "./components/DialogWindow.vue";
import CommentForm from "./components/CommentForm.vue";
import SearchRow from "./components/SearchRow.vue";
import SortSelect from "./components/SortSelect.vue";
export default {
	components: {
		CommentsList,
		DialogWindow,
		CommentForm,
		SearchRow,
		SortSelect,
	},
	data() {
		return {
			comments: [],
			showDialog: false,
			sortOptions: [
				{ value: "name", text: "По имени (А-Я)" },
				{ value: "nameUp", text: "По имени (Я-А)" },
				{ value: "email", text: "По Email (А-Я)" },
				{ value: "emailUp", text: "По Email (Я-А)" },
				{ value: "body", text: "По содержанию (А-Я)" },
				{ value: "bodyUp", text: "По содержанию (Я-А)" },
			],
			selectedOption: "",
			term: "",
		};
	},
	methods: {
		async fetchComments() {
			const rez = await fetch("https://jsonplaceholder.typicode.com/comments");
			this.comments = await rez.json();
		},
		deleteComment(id) {
			this.comments = this.comments.filter((item) => item.id != id);
		},
		addComment(name, email, text) {
			if (name && email && text) {
				this.comments.unshift({
					id: Date.now(),
					name: name,
					email: email,
					body: text,
				});
				this.showDialog = false;
			}
		},
		openDialog() {
			this.showDialog = true;
		},
	},
	computed: {
		searchComments() {
			return this.sortElements.filter(
				(comment) =>
					comment.name.toLowerCase().includes(this.term.toLowerCase()) || comment.body.toLowerCase().includes(this.term.toLowerCase())
			);
		},
		sortElements() {
			if (
				this.selectedOption === "name" ||
				this.selectedOption === "email" ||
				this.selectedOption === "body"
			) {
				return [...this.comments].sort((c1, c2) =>
					c1[this.selectedOption].localeCompare(c2[this.selectedOption])
				);
			} else if (this.selectedOption === "nameUp") {
				return [...this.comments].sort((c1, c2) =>
					c2["name"].localeCompare(c1["name"])
				);
			} else if (this.selectedOption === "emailUp") {
				return [...this.comments].sort((c1, c2) =>
					c2["email"].localeCompare(c1["email"])
				);
			} else if (this.selectedOption === "bodyUp") {
				return [...this.comments].sort((c1, c2) =>
					c2["body"].localeCompare(c1["body"])
				);
			} else {
				return [...this.comments];
			}
		},
	},
	mounted() {
		this.fetchComments();
	},
};
</script>

<style scoped>
</style>
