<template>
	<div class="claimWrapper">
		<h1>Cinemify</h1>
		<p>Hey cinephile! Welcome to the movie search engine.</p>
		<p>Type a part or a full title to get informations about your favourite movies.</p>
	</div>
</template>

<script>
export default {
	name: 'Claim',
}
</script>

<style lang="scss" scoped>

	.claimWrapper {
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: center;
		margin-top: 50px;

		@media (min-width: 768px) {
			margin-top: 150px;
		}
	}
	
	h1 {
		color: white;

		text-shadow: 0 0 5px #fff, 
					0 0 10px #fff, 
					0 0 15px #50C878, 
					0 0 20px #50C878, 
					0 0 25px #50C878, 
					0 0 30px #50C878, 
					0 0 35px #50C878;

		text-transform: uppercase;
		font-size: 70px;
		font-weight: 600;

		@media (min-width: 768px) {
			font-size: 120px;
		}
		
	}

	p {
		color: white;
		text-align: center;
		width: 80%;
		margin-top: 30px;
		font-size: 14px;

		@media (min-width: 768px) {
			font-size: 22px;
			margin-top: 30px;
		}
	}

	p:first-of-type {
		margin-top: 50px;

		@media (min-width: 1280px) {
			margin-top: 70px;
		}
	}

</style>