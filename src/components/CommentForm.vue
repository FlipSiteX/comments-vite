<template>
	<form class="bg-white w-1/3 p-6 rounded-lg">
		<div class="mb-4">
			<h3 class="font-os text-xl font-bold">Новый комментарий</h3>
		</div>

		<div class="mb-4">
			<label for="name"
				class="block text-purple-800 font-medium mb-1"
			>
				Имя
			</label>
			<input type="text" id="name" name="name" v-model="name" required
				class="border-2 border-purple-600 p-2 w-full rounded"
			/>
		</div>

		<div class="mb-4">
			<label for="name"
				class="block text-purple-800 font-medium mb-1"
			>
				Email
			</label>
			<input type="email" id="name" name="name" v-model="email" required
				class="border-2 border-purple-600 p-2 w-full rounded"
			/>
		</div>

		<div class="mb-4">
			<label for="comment"
				class="block text-purple-800 font-medium mb-1"
			>
				Сообщение
			</label>
			<textarea id="comment" name="comment" v-model="body" required
				class="border-2 border-purple-600 min-h-24 max-h-72 p-2 w-full rounded"
			></textarea>
		</div>

		<h3
			v-if="!isFilled"
			class="mb-4 font-medium text-[#ff4242]"
		>
			Заполните все поля
		</h3>

		<button type="button"
			class="bg-purple-600 text-white font-medium py-2 px-4 rounded hover:bg-purple-500"
			@click="name && email && body ? $emit('addComment', name, email, body) : isFilled = false"
		>
			Отправить
		</button>
	</form>
</template>

<script>
export default {
	data() {
		return {
			name: "",
			email: "",
			body: "",
			isFilled: true,
		};
	},
};
</script>

<style></style>