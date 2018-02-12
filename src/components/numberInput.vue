<template>
	<div>
		<div class="ui action input">
			<input @keyup.enter="handleClick" v-model="fibonacciLimitInput" type="text" placeholder="Enter a number">
			<button @click="handleClick" class="ui button">Submit</button>
		</div>

		<div v-if="invalidInput" class="ui negative message">
			<div class="header">
				Please enter a number greater than 1.
			</div>
		</div>
	</div>
</template>

<script>

export default {
	name: 'numberInput',
	data: function() {
		return {
			fibonacciLimitInput: "",
			invalidInput: false,
		}
	},
	methods: {
		handleClick: function(e) {
			if (this.fibonacciLimitInput === "" ||
			this.fibonacciLimitInput < 2) {
				this.invalidInput = true;
				return;
			}
			this.invalidInput = false;
			const seq = getFiobacciSequence(this.fibonacciLimitInput);
			this.$emit('newSequence', {numberEntered: this.fibonacciLimitInput, seq})
			this.fibonacciLimitInput= "";
			return;
		}
	}
}

// https://medium.com/developers-writing/fibonacci-sequence-algorithm-in-javascript-b253dc7e320e
function getFibonacciIndex(num){
	var a = 1, b = 0, temp;

	while (num >= 0) {
		temp = a;
		a = a + b;
		b = temp;
		num--;
	}

	return b;
}

// wrapper function
function getFiobacciSequence(fibonacciLimit) {
	let ind = 1;
	let lastValue = 1;
	let seq = [{
		val: 1,
		even: false,
	}];

	while (lastValue < fibonacciLimit) {
		seq.push({
			val: lastValue,
			even: lastValue % 2 === 0,
		});
		ind++;
		lastValue = getFibonacciIndex(ind)
		}
	return seq
}
</script>
