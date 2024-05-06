<template>
	<!-- Sample Comment 1 -->
	<div
		class="flex bg-white justify-between mt-3 p-4 border rounded-lg border-slate-300"
	>
		<div class="flex">
			<div
				class="w-14 h-14 rounded-full bg-purple-400/50 flex-shrink-0 flex justify-center items-center"
			>
				<i class="fa-solid fa-user text-2xl text-purple-800"></i>
			</div>

			<div class="ml-4">
				<div class="font-medium text-purple-800">
					<p class="break-words">
						{{ comment.name }}
					</p>
				</div>
				<div class="text-gray-600">
					<p class="break-words">
						{{ comment.email }}
					</p>
				</div>
				<div class="mt-2 text-purple-800">
					<p class="break-words">
						{{ comment.body }}
					</p>
				</div>
			</div>
		</div>

		<div @click="$emit('remove', comment.id)">
			<i
				class="fa-solid fa-trash ml-2 cursor-pointer text-slate-400 hover:text-[#ff4242]"
			></i>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		comment: {
			type: Object,
			required: true,
		},
	},
};
</script>

<style scoped></style>
