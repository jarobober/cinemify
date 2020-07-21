<template>
	<div class="aboutWrapper">
		<h2>Hey! I'm Jaro,</h2>
		<p class="text">
			a begginer front-end developer. This project was made to practice my skills in Vue.js framework and connecting REST API using Axios.
		</p>
		<h3>Go to:</h3>
		<ul>
			<li><a href="https://jarobober.github.io/portfolio2.0/"  target="_blank"><img class="briefcase" src="../assets/briefcase.svg">my portfolio</a></li>
			<li><a href="https://github.com/jarobober/"  target="_blank"><img class="github" src="../assets/logo-github.svg">my github</a></li>
		</ul>
		<div class="close" @click="$emit('closeAbout')" />
	</div>
</template>

<script>
export default {
	name: 'About',
}
</script>

<style lang="scss" scoped>
	
	.aboutWrapper {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgb(100, 100, 100);
		padding: 50px;
		font-size: 22px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		color: rgb(209, 209, 209);

		@media (min-width: 768px) {
			width: 60%;
			height: 50%;
			right: 0;
			bottom: 0;
			margin: auto;
			box-shadow: 0 30px 30px -10px rgba(0, 0, 0, 0.3);
		}

		@media (min-width: 1024px) {
			width: 50%;
			height: 50%;
			right: 0;
			bottom: 0;
			margin: auto;
			box-shadow: 0 30px 30px -10px rgba(0, 0, 0, 0.3);
		}

		@media (min-width: 1920px) {
			width: 50%;
			height: 40%;
			padding: 50px 70px;
		}

		h3 {
			margin-top: 10px;

			@media (min-width: 1920px) {
				margin-top: 20px;
			}
		}

		.text {
			margin-top: 10px;

			@media (min-width: 1920px) {
				margin-top: 20px;
			}
		}

		ul {
			list-style: none;

			li {
				margin-top: 10px;

				a {
					color: rgb(209, 209, 209);

					.briefcase, .github {
						position: relative;
						top: 15px;
						margin-right: 10px;
						width: 40px;
						height: auto;
						color: rgb(209, 209, 209);
					}
				}
			}
		}

		
	}

	.close {
	position: absolute;
	width: 30px;
	height: 30px;
	padding: 30px;
	right: 0;
	top: 0;
	cursor: pointer;

		&::before,
		&::after {
		position: absolute;
		top: 30px;
		right: 20px;
		content: '';
		width: 20px;
		height: 2px;
		background: black;
		display: block;
		}

		&::before {
		transform: rotate(45deg);
		}

		&::after {
		transform: rotate(-45deg);
		}
	}
</style>