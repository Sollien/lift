<template>
	<n-config-provider
		:theme="darkTheme"
		class="config-provider"
	>
		<header class="site-header">
			<img
				src="./assets/pwr_logo.svg"
				class="logo"
			/>
			<div class="relative">
				<h1>PWR</h1>
				<span class="h1-echo">PWR</span>
				<span class="h1-echo">PWR</span>
			</div>
		</header>
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

<style scoped lang="scss">
.config-provider {
	display: flex;
	align-items: center;
	flex-direction: column;
}

.main-content {
	min-width: 100%;
	width: 100%;
}

.site-header {
	display: flex;
	align-items: center;
	width: 100%;
	height: 50px;
	margin-bottom: 40px;
	padding: 0 0 10px 0;
	border-bottom: 1px solid rgb(58, 58, 58);

	.logo {
		width: 50px;
	}

	h1 {
		position: relative;
		text-align: left;
		color: #FFB930;
		font-family: 'Bangers', cursive;
		font-size: 3em;
	}

	.h1-echo {
		position: absolute;
		top: 32px;
		left: 5px;
		font-family: 'Bangers', cursive;
		font-size: 3em;
		font-weight: bold;
		line-height: 1.1;
		text-align: left;
		color: #ffba3081;
		z-index: -1;

		&:nth-of-type(2) {
			color: #ffba301a;
			top: 36px;
			left: 9px;
			z-index: -2;
		}
	}
}

@media only screen and (min-width: 768px) {
	.main-content {
		max-width: 700px;
		min-width: 300px;
		width: 700px;
	}

	.site-header {
		height: 80px;
	}
}
</style>
