<template>
	<template
		v-for="exercise in props.day.exercises"
	>
		<h3>{{ exercise.name }}</h3>
		<n-table>
			<thead>
				<tr>
					<th>Set</th>
					<th>Intensity</th>
					<th>Kg</th>
					<th>Reps</th>
					<th></th>
				</tr>
			</thead>
			<tbody>
				<tr
					v-for="(index) in exerciseSets(exercise.isAccessory)"
					:key="index"
				>
					<td>{{ index }}</td>
					<td>
						<template v-if="!exercise.isAccessory">{{ exerciseIntensity[index - 1] }}</template>
						<template v-else-if="exercise.isAccessory && props.weekId !== 4">50</template>
						<template v-else>40</template>%
					</td>
					<td>
						<n-input-number
							v-if="!exercise.isAccessory"
							:placeholder="intensityWeight(exerciseIntensity[index - 1], exercise.name)"
							class="table-number-input"
							:show-button="false"
						></n-input-number>
						<n-input-number
							v-else-if="exercise.isAccessory && props.weekId !== 4"
							:placeholder="intensityWeight(50, exercise.name)"
							class="table-number-input"
							:show-button="false"
						></n-input-number>
						<n-input-number
							v-else
							:placeholder="intensityWeight(40, exercise.name)"
							class="table-number-input"
							:show-button="false"
						></n-input-number>
					</td>
					<td>
						<n-input-number
							v-if="!exercise.isAccessory && exerciseTarget"
							:placeholder="exerciseTarget[index - 1].toString()"
							class="table-number-input"
							:show-button="false"
						></n-input-number>
						<n-input-number
							v-else
							placeholder="10"
							class="table-number-input"
							:show-button="false"
						></n-input-number>
					</td>
					<td>
						<n-checkbox size="large" />
					</td>
				</tr>
			</tbody>
		</n-table>
	</template>
</template>

<script lang="ts" setup>
import { NTable, NInputNumber, NCheckbox } from 'naive-ui'
import { computed } from 'vue'

interface Props {
	oneRm: {
		squat: number,
		deadlift: number,
		bench: number,
		overhead: number,
		pulldown: number,
		row: number
	}
	weekId: number
	day: {
		dayId: number
		exercises: {
			name: string
			isAccessory: boolean
		}[]
	}
}

const props = defineProps<Props>()

function intensityWeight(percent: number, exerciseName: any): string {
		let x: number = 0

		if (exerciseName === "Squat") x = props.oneRm.squat
		else if (exerciseName === "Deadlift") x = props.oneRm.deadlift
		else if (exerciseName === "Bench press") x = props.oneRm.bench
		else if (exerciseName === "Lat pulldown") x = props.oneRm.pulldown
		else if (exerciseName === "Overhead press") x = props.oneRm.overhead
		else if (exerciseName === "Bent-over row") x = props.oneRm.row

		const roundToTwoPointFive = Math.floor(((x * percent) / 100) / 2.5) * 2.5

		return roundToTwoPointFive.toString()
}

function exerciseSets(isAccessory: boolean) {
	if (isAccessory) return 7
	else return 8
}

const exerciseIntensity = computed(() => {
	if (props.weekId === 1) return [65, 75, 85, 65, 65, 65, 65, 65]
	else if (props.weekId === 2) return [70, 80, 90, 70, 70, 70, 70, 70]
	else if (props.weekId === 3) return [75, 85, 95, 75, 75, 75, 75, 75]
	else return [40, 50, 60, 40, 40, 40, 40, 40]
})

const exerciseTarget = computed(() => {
	if (props.weekId === 1 || props.weekId === 4) return [5, 5, 5, 5, 5, 5, 5, 5]
	else if (props.weekId === 2) return [3, 3, 3, 5, 5, 5, 5, 5]
	else if (props.weekId === 3) return [5, 3, 1, 5, 5, 5, 5, 5]
})
</script>

<style lang="scss" scoped>
h3 {
	text-align: left;
}

.table-number-input {
	width: 50px;
}
</style>