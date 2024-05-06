<template>
	<select
		@change="$emit('update:modelValue', $event.target.value)"
		class="flex-1 px-1 outline-none rounded border border-slate-300 focus:border-slate-600"
	>
		<option
			disabled
			selected
		>
			Выберите сортировку
		</option>
		<option value="">Без сортировки</option>
		<option
			v-for="option in sortOptions"
			:value="option.value"
		>
			{{ option.text }}
		</option>
	</select>
</template>

<script>
export default {
	props: {
		sortOptions: {
			type: Object,
			required: true,
		},
		modelValue: {
			type: String,
			default: "",
			required: true
		}
	},
};
</script>

<style scoped></style>
