<template>
	<input
		type="search"
		class="h-full flex-1 px-2 rounded border outline-none focus:border-slate-600 border-slate-300"
		placeholder="Поиск..."
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
	/>
</template>

<script>
export default {
    props: {
        modelValue: {
            type: String
        }
    }
};
</script>

<style scoped>
</style>