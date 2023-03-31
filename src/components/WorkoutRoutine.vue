<template>
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
			<n-tabs type="segment">
				<n-tab-pane
					v-for="day in week.programDays"
					:name="day.dayId"
					:tab="'Day ' + day.dayId"
				>
					<Exercise
						:day="day"
					/>
				</n-tab-pane>
			</n-tabs>
		</n-tab-pane>
	</n-tabs>
</template>

<script setup lang="ts">
import { reactive } from 'vue'
import { NTabs, NTabPane } from 'naive-ui'
import Exercise from './Exercise.vue'

interface Exercise {
	name: string,
	oneRm: number | null
	intensity: number | number[],
	target: number | number[]
	sets: number
}

interface ProgramDay {
	dayId: number
	exercises: Exercise[]
}

interface WeekProgram {
	id: number
	name: string,
	programDays: ProgramDay[]
}

class State {
	public intensityOne: number[] = [65, 75, 85, 65, 65, 65, 65, 65]
	public intensityTwo: number[] = [70, 80, 90, 70, 70, 70, 70, 70]
	public intensityThree: number[] = [75, 85, 95, 75, 75, 75, 75, 75]
	public intensityDeload: number[] = [40, 50, 60, 40, 40, 40, 40, 40]

	public deadliftRm: number | null = null
	public squatRm: number | null = null
	public benchRm: number | null = null
	public overheadRm: number | null = null
	public pulldownRm: number | null = null
	public rowRm: number | null = null

	public intensityDeloadAccessory: number = 30
	public intensityAccessory: number = 50
	public primarySets: number = 8
	public accessorySets: number = 5
	public repsOne: number = 5
	public repsTwo: number[] = [3, 3, 3, 5, 5, 5, 5, 5]
	public repsThree: number[] = [5, 3, 1, 5, 5, 5, 5, 5]
	public repsAccessory: number = 10
	public weeklyProgram: WeekProgram[] = [
		{
			id: 1,
			name: "Week 1",
			programDays: [
				{
					dayId: 1,
					exercises: [
						{
							name: "Squat",
							oneRm: this.squatRm,
							intensity: this.intensityOne,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Bench press",
							oneRm: this.benchRm,
							intensity: this.intensityOne,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Lat pulldowns",
							oneRm: this.pulldownRm,
							intensity: this.intensityAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
				{
					dayId: 2,
					exercises: [
						{
							name: "Deadlift",
							oneRm: this.deadliftRm,
							intensity: this.intensityOne,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Overhead press",
							oneRm: this.overheadRm,
							intensity: this.intensityOne,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Bent-over rows",
							oneRm: this.rowRm,
							intensity: this.intensityAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
				{
					dayId: 3,
					exercises: [
						{
							name: "Bench press",
							oneRm: this.benchRm,
							intensity: this.intensityOne,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Squat",
							oneRm: this.squatRm,
							intensity: this.intensityOne,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Lat pulldowns",
							oneRm: this.pulldownRm,
							intensity: this.intensityAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
			]
		},
		{
			id: 2,
			name: "Week 2",
			programDays: [
				{
					dayId: 1,
					exercises: [
						{
							name: "Squat",
							oneRm: this.squatRm,
							intensity: this.intensityTwo,
							target: this.repsTwo,
							sets: this.primarySets
						},
						{
							name: "Bench press",
							oneRm: this.benchRm,
							intensity: this.intensityTwo,
							target: this.repsTwo,
							sets: this.primarySets
						},
						{
							name: "Lat pulldowns",
							oneRm: this.pulldownRm,
							intensity: this.intensityAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
				{
					dayId: 2,
					exercises: [
						{
							name: "Deadlift",
							oneRm: this.deadliftRm,
							intensity: this.intensityTwo,
							target: this.repsTwo,
							sets: this.primarySets
						},
						{
							name: "Overhead press",
							oneRm: this.overheadRm,
							intensity: this.intensityTwo,
							target: this.repsTwo,
							sets: this.primarySets
						},
						{
							name: "Bent-over rows",
							oneRm: this.pulldownRm,
							intensity: this.intensityAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
				{
					dayId: 3,
					exercises: [
						{
							name: "Bench press",
							oneRm: this.benchRm,
							intensity: this.intensityTwo,
							target: this.repsTwo,
							sets: this.primarySets
						},
						{
							name: "Squat",
							oneRm: this.squatRm,
							intensity: this.intensityTwo,
							target: this.repsTwo,
							sets: this.primarySets
						},
						{
							name: "Lat pulldowns",
							oneRm: this.pulldownRm,
							intensity: this.intensityAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
			]
		},
		{
			id: 3,
			name: "Week 3",
			programDays: [
				{
					dayId: 1,
					exercises: [
						{
							name: "Squat",
							oneRm: this.squatRm,
							intensity: this.intensityThree,
							target: this.repsThree,
							sets: this.primarySets
						},
						{
							name: "Bench press",
							oneRm: this.benchRm,
							intensity: this.intensityThree,
							target: this.repsThree,
							sets: this.primarySets
						},
						{
							name: "Lat pulldowns",
							oneRm: this.pulldownRm,
							intensity: this.intensityAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
				{
					dayId: 2,
					exercises: [
						{
							name: "Deadlift",
							oneRm: this.deadliftRm,
							intensity: this.intensityThree,
							target: this.repsThree,
							sets: this.primarySets
						},
						{
							name: "Overhead press",
							oneRm: this.overheadRm,
							intensity: this.intensityThree,
							target: this.repsThree,
							sets: this.primarySets
						},
						{
							name: "Bent-over rows",
							oneRm: this.rowRm,
							intensity: this.intensityAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
				{
					dayId: 3,
					exercises: [
						{
							name: "Bench press",
							oneRm: this.benchRm,
							intensity: this.intensityThree,
							target: this.repsThree,
							sets: this.primarySets
						},
						{
							name: "Squat",
							oneRm: this.squatRm,
							intensity: this.intensityThree,
							target: this.repsThree,
							sets: this.primarySets
						},
						{
							name: "Lat pulldowns",
							oneRm: this.pulldownRm,
							intensity: this.intensityAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
			]
		},
		{
			id: 4,
			name: "Deload",
			programDays: [
				{
					dayId: 1,
					exercises: [
						{
							name: "Squat",
							oneRm: this.squatRm,
							intensity: this.intensityDeload,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Bench press",
							oneRm: this.benchRm,
							intensity: this.intensityDeload,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Lat pulldowns",
							oneRm: this.pulldownRm,
							intensity: this.intensityDeloadAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
				{
					dayId: 2,
					exercises: [
						{
							name: "Deadlift",
							oneRm: this.deadliftRm,
							intensity: this.intensityDeload,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Overhead press",
							oneRm: this.overheadRm,
							intensity: this.intensityDeload,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Bent-over rows",
							oneRm: this.rowRm,
							intensity: this.intensityDeloadAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
				{
					dayId: 3,
					exercises: [
						{
							name: "Bench press",
							oneRm: this.benchRm,
							intensity: this.intensityDeload,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Squat",
							oneRm: this.squatRm,
							intensity: this.intensityDeload,
							target: this.repsOne,
							sets: this.primarySets
						},
						{
							name: "Lat pulldowns",
							oneRm: this.pulldownRm,
							intensity: this.intensityDeloadAccessory,
							target: this.repsAccessory,
							sets: this.accessorySets
						}
					]
				},
			]
		},
	]
}

const state = reactive(new State())
</script>

<style scoped lang="scss">
h3 {
	text-align: left;
}
</style>