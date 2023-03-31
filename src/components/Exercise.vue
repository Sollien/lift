<template>
	<template v-for="exercise in props.day.exercises">
		<h3>{{ exercise.name }}</h3>
		<div class="input-label-container">
			<label>Enter 1RM</label>
			<n-input-number
				v-model:value="exercise.oneRm"
				placeholder="Enter 1RM..."
				class="rm-input"
			/>
		</div>
		<n-table>
			<thead>
				<tr>
					<th>Set</th>
					<th>Intensity</th>
					<th>Target</th>
					<th>Kg</th>
					<th>Reps</th>
					<th></th>
				</tr>
			</thead>
			<tbody>
				<tr
					v-for="(set, index) in exercise.sets"
					:key="index"
				>
					<td>{{ set }}</td>
					<td v-if="Array.isArray(exercise.intensity)">{{ exercise.intensity[index] }}%</td>
					<td v-else>{{ exercise.intensity }}%</td>
					<td v-if="Array.isArray(exercise.target)">{{ exercise.target[index] }} reps</td>
					<td v-else>{{ exercise.target }} reps</td>
					<td>
						<n-input-number
							v-if="Array.isArray(exercise.intensity)"
							:placeholder="intensityWeight(exercise.intensity[index], exercise.oneRm)"
							class="table-number-input"
						></n-input-number>
						<n-input-number
							v-else
							:placeholder="intensityWeight(exercise.intensity, exercise.oneRm)"
							class="table-number-input"
						></n-input-number>
					</td>
					<td>
						<n-input-number
							v-if="Array.isArray(exercise.target)"
							:placeholder="exercise.target[index].toString()"
							class="table-number-input"
						></n-input-number>
						<n-input-number
							v-else
							:placeholder="exercise.target.toString()"
							class="table-number-input"
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
import { reactive, computed } from 'vue'

interface Props {
	day: {
		dayId: number
		exercises: {
			name: string
			oneRm: number | null
			intensity: number | number[]
			target: number | number[]
			sets: number
		}[]
	}
}

const props = defineProps<Props>()

class State {
	public oneRm: number | null = null
	public target: number = 5
}

function intensityWeight(percent: number, oneRm: number | null): string {
	if (oneRm !== null) {
		const roundToTwoPointFive = Math.floor(((oneRm * percent) / 100) / 2.5) * 2.5
		return roundToTwoPointFive.toString()
	} else {
		return "0"
	}
}

const targetToString = computed(() => {
	const stringValue = state.target
	return stringValue.toString()
})

const state = reactive(new State())
</script>

<style lang="scss" scoped>
h3 {
	text-align: left;
}

.input-label-container {
	margin-bottom: 10px;
	text-align: left;

	.rm-input {
		margin-top: 5px;
	}
}

.table-number-input {
	width: 100px;
}
.table-number-input {
	width: 100px;
}
</style>