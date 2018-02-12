<template>
	<div class="ui container">
		<h1>
			Fibonacci App <i class="calculator icon"></i>
		</h1>
		<h2>
			About
		</h2>
		<div class="content">
			<p>
				This app will summate the even numbers of the <a href="https://www.mathsisfun.com/numbers/fibonacci-sequence.html">fibonacci sequence</a> that are less than the provided value.
			</p>
			<p>
				Type in a value and <strong>press enter</strong> or <strong>click submit</strong> to see the sequence and its sum.
			</p>
		</div>
		<NumberInput v-on:newSequence="addSequence" />
		<SequenceResults v-if="fibonacciSequences.length" :sequences="fibonacciSequences" />
		<div class="ui hidden divider"></div>
		<div class="source">
			<a class="ui right labeled icon black button" href="https://github.com/ajschmidt8/fibonacci" target="_blank">
				<i class="right github icon"></i>
				Source Code
			</a>
		</div>
	</div>
</template>

<script>
import NumberInput from './components/numberInput';
import SequenceResults from './components/sequenceResults';
import uuid from 'uuid/v1';

export default {
	name: 'app',
	data() {
		return {
			fibonacciSequences: []
		}
	},
	methods: {
		addSequence(seq) {
			this.fibonacciSequences.push({key: uuid(), ...seq});
		},
	},
	components: {
		NumberInput,
		SequenceResults
	}
}
</script>

<style scoped lang="scss">
	h1 {
		margin: 2em 0 1em;
		text-align: center;
	}

	h2 {
		margin-bottom: 0.2em;
	}

	.content {
		margin-bottom: 2em;
	}

	.source {
		text-align: right;
	}
</style>
