<template>
	<n-config-provider :theme="darkTheme">
		<WorkoutRoutine />
	</n-config-provider>
</template>

<script setup lang="ts">
import WorkoutRoutine from './components/WorkoutRoutine.vue'
import { NConfigProvider } from 'naive-ui'
import { darkTheme } from 'naive-ui'
</script>

<style scoped>
.logo {
	height: 6em;
	padding: 1.5em;
	will-change: filter;
	transition: filter 300ms;
}
.logo:hover {
	filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
	filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
