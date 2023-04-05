<template>
	<n-config-provider :theme="darkTheme">
		<div class="main-content">
			<WorkoutRoutine />
		</div>
	</n-config-provider>
</template>

<script setup lang="ts">
import WorkoutRoutine from './views/WorkoutRoutine.vue'
import { NConfigProvider } from 'naive-ui'
import { darkTheme } from 'naive-ui'
</script>

<style scoped>

.main-content {
	min-width: 100%;
	width: 100%;
}

@media only screen and (min-width: 768px) {
	.main-content {
		max-width: 700px;
		min-width: 300px;
		width: 700px;
	}
}
</style>
