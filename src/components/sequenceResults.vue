<template>
	<div>
		<div class="ui hidden divider"></div>
		<table class="ui celled table">
			<thead>
				<tr>
					<th class="center aligned">Number Entered</th>
					<th class="center aligned">Sequence</th>
					<th class="center aligned">Sum</th>
				</tr>
			</thead>

			<tbody>
				<tr v-for="sequence in sequences" :key="sequence.id">
					<td class="center aligned numberEntered">
						{{ sequence.numberEntered }}
					</td>
					<td v-html="getSequenceString(sequence.seq)" class="center aligned sequence">

					</td>
					<td class="center aligned">
						{{ getSequenceSum(sequence.seq) }}
					</td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
export default {
	name: 'inputResults',
	props: ['sequences'],
	methods: {
		getSequenceString(seq) {
			return seq.reduce((seqStr, seqItem) => {
				return seqStr += seqItem.even ? `<span class="sequenceEven">${seqItem.val}</span> ` : `${seqItem.val} `
			}, "");
		},
		getSequenceSum(seq) {
			return seq.reduce((sum, seqItem) => {
				return seqItem.even ? sum += seqItem.val : sum += 0;
			}, 0)
		}
	}
}
</script>

<style lang="scss">
	.sequence {
		word-spacing: 18px;
	}
	.sequenceEven {
		font-weight: 700;
		color: green;
		text-decoration: underline;
	}
	.numberEntered {
		font-weight: 400!important;
	}
</style>

