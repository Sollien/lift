<template>
	<n-tabs type="segment">
		<n-tab-pane
			v-for="day in state.programDays"
			:name="day.dayId"
			:tab="'Day ' + day.dayId"
		>
			<Exercise
				:day="day"
				:weekId="props.week.id"
				:oneRm="props.oneRm"
			/>
		</n-tab-pane>
	</n-tabs>
</template>

<script lang="ts" setup>
import { reactive, defineAsyncComponent } from 'vue'
import { NTabs, NTabPane } from 'naive-ui'

interface Exercise {
	name: string,
	isAccessory: boolean
}

interface ProgramDay {
	dayId: number
	exercises: Exercise[]
}

interface Props {
	oneRm: {
		squat: number,
		deadlift: number,
		bench: number,
		overhead: number,
		pulldown: number,
		row: number
	}
	week: {
		id: number,
		name: string,
	},
}

const props = defineProps<Props>()

class State {
	public loading: boolean = false

	public programDays: ProgramDay[] = [
		{
			dayId: 1,
			exercises: [
				{
					name: "Squat",
					isAccessory: false
				},
				{
					name: "Bench press",
					isAccessory: false
				},
				{
					name: "Lat pulldown",
					isAccessory: true
				}
			]
		},
		{
			dayId: 2,
			exercises: [
				{
					name: "Deadlift",
					isAccessory: false
				},
				{
					name: "Overhead press",
					isAccessory: false
				},
				{
					name: "Bent-over row",
					isAccessory: true
				}
			]
		},
		{
			dayId: 3,
			exercises: [
				{
					name: "Bench press",
					isAccessory: false
				},
				{
					name: "Squat",
					isAccessory: false
				},
				{
					name: "Lat pulldowns",
					isAccessory: true
				}
			]
		},
	]
}

const state = reactive(new State())

state.loading = true

const Exercise = defineAsyncComponent(() =>
  import('./Exercise.vue')
)
</script>