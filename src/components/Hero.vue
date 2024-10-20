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
			<div class="hero__carousel">
				<p v-if="$i18n.locale != 'uz'">{{ $t('for') }}</p>
				<div class="hero__carousel-container" :class="{ alignright: $i18n.locale == 'uz' }">
					<p
						v-for="(text, i) in [
							$t('for-uni'),
							$t('for-school'),
							$t('for-centres'),
							$t('for-business')
						]"
						:key="i"
						:class="{ active: i == carouselIndex }">
						{{ text }}
					</p>
				</div>
				<p v-if="$i18n.locale == 'uz'">{{ $t('for') }}</p>
			</div>
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
	</section>
</template>

<script setup>
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { computed, onMounted, ref } from 'vue';
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

const carouselIndex = ref(0);

onMounted(() => {
	const seconds = 1.5;
	setInterval(() => {
		carouselIndex.value = (carouselIndex.value + 1) % 4;
	}, seconds * 1000);
});
</script>

<style lang="scss" scoped>
body.preloader-active {
	.hero__title,
	.hero__text,
	.hero__stats,
	.hero__carousel {
		animation-play-state: paused;
	}
}
.hero {
	min-height: 100vh;
	background-image: linear-gradient(to right bottom, var(--blue), #061f35);
	background-repeat: no-repeat;
	background-size: cover;
	background-position: center;
	position: relative;

	overflow: visible !important;
	display: grid;
	grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
	gap: max(6vw, 5rem);
	@media only screen and (max-width: 768px) {
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
	}

	&__carousel {
		font-size: 5rem;
		text-transform: uppercase;
		display: flex;
		gap: 1.5rem;
		animation: fade-rotate 800ms both 600ms;
		@media only screen and (max-width: 768px) {
			font-size: 3rem;
		}
		@media only screen and (max-width: 500px) {
			font-size: 2rem;
		}
		&-container {
			display: grid;
			text-align: left;
			&.alignright {
				text-align: right;
			}
			p {
				opacity: 0;
				transform: translateX(10rem);
				transition: opacity 0.5s, transform 0.5s, display 0.5s;
				transition-behavior: allow-discrete;
				grid-area: 1/1/2/2;
				&.active {
					opacity: 1;
					transform: translateX(0);
				}
			}
		}
	}

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
		animation: fade-rotate 800ms forwards 1s;
		justify-content: center;
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
			@media only screen and (min-width: 1920px) {
				font-size: 4rem;
			}
		}
		&-text {
			opacity: 0.5;
			font-size: 1.7rem;
			@media only screen and (min-width: 1920px) {
				font-size: 2.5rem;
			}
		}
		&-divider {
			align-self: stretch;
			border-top: 1px solid var(--yellow);
		}
	}

	&__text {
		font-size: 1.8rem;
		font-weight: 300;
		font-family: var(--font-base);
		opacity: 0;
		line-height: 1.5;
		animation: fade-rotate-2 800ms forwards 200ms;

		@media only screen and (min-width: 1920px) {
			font-size: 2.2rem;
			display: none;
		}
	}
	&__title {
		font-size: 7.5rem;
		line-height: 1.1;
		font-weight: 600;
		text-transform: uppercase;
		animation: fade-rotate 800ms forwards;

		@media only screen and (min-width: 1920px) {
			font-size: 7rem;
		}
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
		gap: 4rem;
		font-family: var(--font-alt);
		align-items: center;
		text-align: center;

		@media only screen and (min-width: 1920px) {
			max-width: 80%;
			margin: auto;
		}

		@media only screen and (max-width: 1100px) {
			padding-top: 10rem;
			text-align: center;
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
