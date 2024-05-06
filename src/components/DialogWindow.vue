<template>
	<div v-if="showDialog" class="fixed left-0 top-0 right-0 bottom-0 grid place-items-center backdrop-blur-sm bg-black/50">
        <i @click="$emit('closeDialog')" class="fa-solid fa-square-xmark fixed top-12 right-14 cursor-pointer text-6xl text-slate-400 hover:text-[#ff4242]"></i>
		<slot></slot>
	</div>
</template>

<script>
export default {
    props: {
        showDialog: {
            type: Boolean,
            default: false
        }
    },
};
</script>

<style scoped></style>