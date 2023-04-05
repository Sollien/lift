<template>
	<n-config-provider :theme="darkTheme">
		<div class="main-content">
			<WorkoutRoutine />
		</div>
	</n-config-provider>
</template>

<script setup lang="ts">
import WorkoutRoutine from './components/WorkoutRoutine.vue'
import { NConfigProvider } from 'naive-ui'
import { darkTheme } from 'naive-ui'
</script>

<style scoped>

@media only screen and (min-width: 768px) {
	.main-content {
		max-width: 1000px;
		width: 750px;
	}
}
</style>
