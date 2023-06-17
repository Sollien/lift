<template>
	<n-collapse
		class="rm-collapse"
	>
		<n-collapse-item title="One RM max for exercises" name="1">
			<div class="grid-2-small-gap">
				<div class="input-label-container">
					<label>Squat</label>
					<n-input-number
						v-model:value="state.oneRm.squat"
						placeholder="Enter 1RM..."
						class="rm-input"
					/>
				</div>
				<div class="input-label-container">
					<label>Deadlift</label>
					<n-input-number
						v-model:value="state.oneRm.deadlift"
						placeholder="Enter 1RM..."
						class="rm-input"
					/>
				</div>
				<div class="input-label-container">
					<label>Overhead press</label>
					<n-input-number
						v-model:value="state.oneRm.overhead"
						placeholder="Enter 1RM..."
						class="rm-input"
					/>
				</div>
				<div class="input-label-container">
					<label>Bench press</label>
					<n-input-number
						v-model:value="state.oneRm.bench"
						placeholder="Enter 1RM..."
						class="rm-input"
					/>
				</div>
				<div class="input-label-container">
					<label>Lat pulldown</label>
					<n-input-number
						v-model:value="state.oneRm.pulldown"
						placeholder="Enter 1RM..."
						class="rm-input"
					/>
				</div>
				<div class="input-label-container">
					<label>Bent-over row</label>
					<n-input-number
						v-model:value="state.oneRm.row"
						placeholder="Enter 1RM..."
						class="rm-input"
					/>
				</div>
			</div>
		</n-collapse-item>
	</n-collapse>
	<n-tabs
		type="line"
		animated
	>
		<n-tab-pane
			v-for="week in state.weeklyProgram"
			:key="week.id"
			:name="week.name"
			:tab="week.name"
		>
			<WorkoutWeek
				:week="week"
				:oneRm="state.oneRm"
			/>
		</n-tab-pane>
	</n-tabs>
</template>

<script setup lang="ts">
import { reactive } from 'vue'
import {
	NTabs,
	NTabPane,
	NInputNumber,
	NCollapse,
	NCollapseItem,
} from 'naive-ui'
import WorkoutWeek from '../components/WorkoutWeek.vue'

interface WeekProgram {
	id: number
	name: string,
}

class State {
	public oneRm: {
		squat: number
		deadlift: number
		bench: number
		overhead: number
		pulldown: number
		row: number
	} = {
		squat: 0,
		deadlift: 0,
		bench: 0,
		overhead: 0,
		pulldown: 0,
		row: 0,
	}

	public weeklyProgram: WeekProgram[] = [
		{
			id: 1,
			name: "Week 1",
		},
		{
			id: 2,
			name: "Week 2",
		},
		{
			id: 3,
			name: "Week 3",
		},
		{
			id: 4,
			name: "Deload",
		},
	]
}

const state = reactive(new State())
</script>

<style scoped lang="scss">
h3 {
	text-align: left;
}

.wavy-border {
	display: block;
	margin-bottom: 20px;
	text-align: left;
	font-size: 30px;
	color: #63e2b7;
}

.rm-collapse {
	margin-bottom: 20px;
}

.input-label-container {
	margin-bottom: 10px;
	text-align: left;

	.rm-input {
		margin-top: 5px;
	}
}
</style>