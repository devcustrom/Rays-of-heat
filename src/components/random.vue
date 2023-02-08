<template>
	<div v-if="gender" class="ring-1 ring-pink-400 rounded-xl p-5 text-2xl font-semibold underline decoration-pink-400">
		{{ phrase }}
	</div>
</template>

<script setup>
	import { ref, onBeforeMount } from 'vue'

	const props = defineProps({
		gender: {
			type: String,
			default: () => ''
		}
	})
	const phrase = ref('')

	const getRandom = (arr) => arr[Math.floor(Math.random()*arr.length)]
	onBeforeMount(async () => {
		const response = await (await fetch('/pleasantness.json')).json()
		phrase.value = getRandom(response[props.gender])
	})
</script>