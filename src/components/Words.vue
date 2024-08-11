<template>
	<section class="words">
		<h1 class="words__words">Remember I am the strongest frontend developer</h1>
		<h1 class="words__title">Online learning wherever and whenever.</h1>
	</section>
</template>

<script setup></script>

<style lang="scss" scoped>
.words {
	font-family: var(--font-alt);
	position: relative;
	display: grid;
	place-items: center;
	min-height: 30rem;
	overflow: hidden;
	padding: 0 5vw;
	text-align: center;
	&__title {
		font-size: 4.5rem;
		letter-spacing: -2px;
		font-weight: 600;
	}
	&__words {
		position: absolute;
		font-size: max(13vw, 120px);
		letter-spacing: -2px;
		text-wrap: nowrap;
		z-index: -1;
		animation: move 50s linear infinite alternate;
		mask-image: linear-gradient(
			to right,
			transparent 0,
			#00000010 20%,
			#00000010 80%,
			transparent 100%
		);
	}
}

@keyframes move {
	from {
		transform: translateX(30%);
	}
	to {
		transform: translateX(-50%);
	}
}
</style>
