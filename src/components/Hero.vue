<template>
	<section class="hero section-padding">
		<div class="hero__svg-container">
			<Circle class="hero__svg hero__svg-1" />
			<Rectangle class="hero__svg hero__svg-2" />
			<Triangle class="hero__svg hero__svg-3" />
		</div>
		<div class="hero__lines"></div>
		<div class="hero__content">
			<h1 class="hero__title">{{ $t('hero-title') }}</h1>
			<p class="hero__text">
				{{ $t('hero-text') }}
			</p>
			<div class="hero__stats">
				<div class="hero__stat" v-for="stat in stats" :key="stat.amount">
					<h2 class="hero__stat-name">{{ stat.amount }}+</h2>
					<div class="hero__stat-divider"></div>
					<p class="hero__stat-text">
						{{ stat.name }}
					</p>
				</div>
			</div>
		</div>
		<div
			class="hero__images-container"
			@mousemove="handleMouseMove"
			@mouseleave="handleMouseLeave">
			<div class="hero__images" ref="imgContainerRef">
				<img src="@/assets/images/guy.webp" alt="hero guy" />
			</div>
		</div>
	</section>
</template>

<script setup>
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { computed, ref } from 'vue';
gsap.registerPlugin(ScrollTrigger);
import Circle from '@/components/Circle.vue';
import Rectangle from './Rectangle.vue';
import Triangle from './Triangle.vue';
import { i18n } from '@/locales';

const stats = computed(() => [
	{
		amount: i18n.global.t('hero-stat-amount-1'),
		name: i18n.global.t('hero-stat-name-1')
	},
	{
		amount: i18n.global.t('hero-stat-amount-2'),
		name: i18n.global.t('hero-stat-name-2')
	},
	{
		amount: i18n.global.t('hero-stat-amount-3'),
		name: i18n.global.t('hero-stat-name-3')
	}
]);

const imgContainerRef = ref();

const handleMouseMove = e => {
	const rect = imgContainerRef.value.getBoundingClientRect();
	const x = e.clientX - rect.left - rect.width / 2;
	const y = e.clientY - rect.top - rect.height / 2;

	const rotateX = (-y / rect.height) * 45; // Stronger rotation
	const rotateY = (x / rect.width) * 45;

	gsap.to(imgContainerRef.value, {
		duration: 0.5, // Slightly longer duration for more dramatic effect
		rotateX: rotateX,
		rotateY: rotateY,
		scale: 1.06,
		ease: 'power1.out',
		transformOrigin: 'center'
	});
};
const handleMouseLeave = () => {
	gsap.to(imgContainerRef.value, {
		duration: 0.7, // Slightly longer duration to smoothly reset
		rotateX: 0,
		rotateY: 0,
		translateZ: 0,
		scale: 1,
		ease: 'power1.out'
	});
};
</script>

<style lang="scss" scoped>
.hero {
	min-height: 100vh;
	background-image: linear-gradient(to right bottom, var(--blue), #061f35);
	background-repeat: no-repeat;
	background-size: cover;
	background-position: center;
	position: relative;

	overflow: visible !important;
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	gap: max(6vw, 5rem);

	&__svg {
		width: 3rem;
		height: 3rem;
		bottom: 0;
		left: 0;
		&-container {
			width: 100%;
			height: 100%;
			position: absolute;
			display: grid;
			place-items: center;
		}
	}

	@media only screen and (max-width: 900px) {
		grid-template-columns: none;
		grid-auto-rows: 1fr;
	}
	&__rectangle {
		position: absolute;
		z-index: 1;
		width: 107%;
		height: 107%;
		top: -1rem;
		left: -6px;
	}
	&__obj {
		position: absolute;
		top: -50%;
		left: -20rem;

		@media only screen and (max-width: 900px) {
			top: -40%;
			left: -30rem;
		}
	}
	&__lines {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-image: url('@/assets/images/hero-lines.svg');
		background-size: 12.5rem;
	}
	button {
		border: none;
		cursor: pointer;
		font-family: var(--font-base);
	}
	&__stats {
		display: flex;
		gap: 3rem;
		flex-wrap: wrap;
		opacity: 0;
		animation: fade-rotate 800ms forwards 600ms;
	}
	&__stat {
		display: flex;
		flex-basis: 20%;
		align-items: center;
		flex-direction: column;
		gap: 1rem;
		text-align: center;
		&-name {
			font-size: 3.2rem;
		}
		&-text {
			opacity: 0.5;
			font-size: 1.7rem;
		}
		&-divider {
			align-self: stretch;
			border-top: 1px solid var(--yellow);
		}
	}

	&__text {
		font-size: 18px;
		font-weight: 300;
		font-family: var(--font-base);
		opacity: 0;
		line-height: 1.5;
		animation: fade-rotate-2 800ms forwards 200ms;
	}
	&__title {
		font-size: 7.5rem;
		font-weight: 500;
		line-height: 0.89;
		animation: fade-rotate 800ms forwards;
		@media only screen and (max-width: 767px) {
			font-size: 5rem;
		}
	}
	&__content {
		z-index: 1;
		color: #fff;
		display: flex;
		flex-direction: column;
		justify-content: center;
		gap: 40px;
		font-family: var(--font-alt);

		@media only screen and (max-width: 1100px) {
			padding-top: 10rem;
			text-align: center;
		}
	}
	&__images {
		position: relative;
		width: 100%;
		height: 100%;

		&-container {
			display: flex;
			justify-content: center;
			transform-style: preserve-3d;
		}

		img {
			width: 100%;
			height: 100%;
			object-fit: contain;
			position: relative;
			z-index: 2;
		}
	}
}

@keyframes up-down {
	from {
		transform: translateY(-30px);
	}
	to {
		transform: translateY(30px);
	}
}
@keyframes fade-rotate-2 {
	from {
		opacity: 0;
		transform: rotateY(-100deg) translate(9rem, 9rem);
	}
	to {
		opacity: 0.5;
		transform: rotateY(0) translate(0, 0);
	}
}

@function generate-translate() {
	$x: random(100); // Generates a random number between 0 and 100 for vw
	$y: random(100) * -1; // Generates a random number between 0 and 100 for vh
	@return translate(#{$x}vw, #{$y}vh);
}

@function generate-rotation() {
	@return rotate(#{random(360)}deg);
}

@for $i from 1 through 3 {
	@keyframes wander#{$i} {
		0% {
			transform: translate(0, 0) rotate(0deg);
		}
		10% {
			transform: generate-translate() generate-rotation();
		}
		20% {
			transform: generate-translate() generate-rotation();
		}
		30% {
			transform: generate-translate() generate-rotation();
		}
		40% {
			transform: generate-translate() generate-rotation();
		}
		50% {
			transform: generate-translate() generate-rotation();
		}
		60% {
			transform: generate-translate() generate-rotation();
		}
		70% {
			transform: generate-translate() generate-rotation();
		}
		80% {
			transform: generate-translate() generate-rotation();
		}
		90% {
			transform: generate-translate() generate-rotation();
		}
		100% {
			transform: generate-translate() generate-rotation(); // End at a completely random position
		}
	}

	.hero__svg-#{$i} {
		position: absolute;
		animation: wander#{$i} #{40 + ($i * 2)}s ease-in-out infinite alternate;
	}
}
</style>
