<template>
	<div class="input-label-container">
		<label>Enter your 1RM</label>
		<n-input-number 
			v-model:value="state.oneRm"
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
			<tr>
				<td>1</td>
				<td>65%</td>
				<td>5 reps</td>
				<td>
					<n-input-number
						:placeholder="intensityWeight(65)"
						class="table-number-input"
					></n-input-number>	
				</td>
				<td>
					<n-input-number
						placeholder="5"
						class="table-number-input"
					></n-input-number>
				</td>
				<td></td>
			</tr>
		</tbody>
	</n-table>
</template>

<script setup lang="ts">
import { reactive, computed } from 'vue'
import { NInputNumber, NTable } from 'naive-ui'

type RowData = {
	key: number
	name: string
	age: number
	address: string
	tags: string[]
}

class State {
	public oneRm: number | null = null
}

function intensityWeight(percent: number): string {
	if (state.oneRm !== null) {
		const roundToTwoPointFive = Math.floor(((state.oneRm * percent) / 100) / 2.5) * 2.5
		return roundToTwoPointFive.toString()
	} else {
		return "0"
	}
}

const state = reactive(new State())
</script>

<style scoped lang="scss">
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
</style>
