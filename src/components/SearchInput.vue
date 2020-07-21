<template>
	<input 
		name="search" 
		:class="{ dark }"
		placeholder="type a movie title" 
		:value="value"
		@input="handleChange"
		/>
</template>

<script>


export default {
	name: 'SearchInput',
	props: {
		value: {
			type: String,
			required: true,
		},
		dark: {
				type: Boolean,
				default: false,
			},
	},
	data() {
		return {
			
		};
	},
	methods: {
		handleChange(e) {
			this.$emit('input', e.target.value)
		}
	},
};
</script>

<style lang="scss" scoped>

	input {
		background-color: transparent;
		border: none;
		border-bottom: 1px solid white;
		display: block;
		margin: 50px auto 0 auto;
		transition: box-shadow .3s ease;
		color: white;
		font-family: Montserrat, sans-serif;
		text-align: center;

		@media (min-width: 768px) {
			font-size: 20px;
			margin: 60px auto 0 auto;
		}
	}

	input:focus {
		outline: none;
		box-shadow: 0 10px 12px -4px #50C878;
	}

	input::placeholder {
		color: rgba(255, 255, 255, 0.673);
	}

	.dark {
		color: black;
		border-bottom: 1px solid black;
	}

	.dark:focus {
		outline: none;
		box-shadow: 0 10px 10px -4px grey;
	}

	.dark::placeholder {
		color: rgba(152, 152, 152, 0.9);
	}

</style>