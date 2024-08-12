<template>
	<section class="hero section-padding">
		<img ref="objRef" class="hero__obj" src="@/assets/images/green-object.png" alt="green" />
		<div class="hero__lines"></div>
		<div class="hero__content">
			<h1 class="hero__title">Best online platform for education.</h1>
			<p class="hero__text">
				Online courses from the world's leading experts. Join 17 million learners today.
			</p>
			<div class="hero__cta">
				<Button label="Get started" />
				<button class="hero__youtube">
					<IconYoutube class="hero__youtube-icon--1" />
					<span class="hero__youtube-span">How it works</span>
					<IconYoutube class="hero__youtube-icon" />
				</button>
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
		<div
			class="hero__images-container"
			@mousemove="handleMouseMove"
			@mouseleave="handleMouseLeave">
			<div class="hero__images" ref="imgContainerRef">
				<img src="@/assets/images/hero-guy.webp" alt="hero guy" />
				<img src="@/assets/images/yellow-object.webp" alt="yeellow thingy" />
			</div>
		</div>
	</section>
</template>

<script setup>
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { onMounted, ref } from 'vue';
import IconLike from './icons/IconLike.vue';
import IconYoutube from './icons/IconYoutube.vue';
import Button from './Button.vue';
gsap.registerPlugin(ScrollTrigger);

const stats = [
	{
		amount: 260,
		name: 'Tutors'
	},
	{
		amount: 5340,
		name: 'Students'
	},
	{
		amount: 280,
		name: 'Courses'
	}
];

const imgContainerRef = ref();
const objRef = ref();

onMounted(() => {
	gsap.to(objRef.value, {
		y: 200,
		scrollTrigger: {
			trigger: '.hero',
			scrub: 1,
			start: 'top top'
		}
	});
});

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
	background-image: url('@/assets/images/hero-bg.jpg');
	background-repeat: no-repeat;
	background-size: cover;
	background-position: center;
	position: relative;

	padding-right: 0;
	padding-bottom: 2rem;
	display: grid;
	grid-template-columns: 1fr 2fr;
	overflow: hidden;
	gap: 2rem;

	@media only screen and (max-width: 900px) {
		grid-template-columns: none;
		grid-auto-rows: 1fr;
		padding-bottom: 5rem;
		padding-right: 5vw;
		min-height: 887px;
	}
	&__obj {
		position: absolute;
		top: 15rem;
		left: -10rem;
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
	&__cta {
		display: flex;
		justify-content: center;
		gap: 2rem;
		opacity: 0;
		animation: fade-rotate 800ms forwards 400ms;
	}
	&__youtube {
		background-color: transparent;
		color: #fff;
		display: flex;
		align-items: center;
		gap: 5px;
		&:hover {
			& .hero__youtube-span {
				transform: translateX(-10px);
			}
			& .hero__youtube-icon {
				opacity: 1;
				transform: translateX(-10px);
			}
			& .hero__youtube-icon--1 {
				opacity: 0;
				transform: translateX(-10px);
			}
		}
		&-span {
			transition: transform 300ms;
		}
		&-icon {
			transition: transform 300ms, opacity 300ms;
			opacity: 0;
			transform: translateX(10px);
			&--1 {
				transition: transform 300ms, opacity 300ms;
			}
		}
	}
	&__stats {
		display: flex;
		justify-content: space-between;
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
		&-name {
			font-size: 3.2rem;
		}
		&-text {
			opacity: 0.5;
			font-size: 1.7rem;
		}
		&-divider {
			align-self: stretch;
			border-top: 1px solid var(--base-color);
		}
	}

	&__text {
		font-size: 18px;
		font-weight: 300;
		font-family: var(--font-base);
		opacity: 0;
		animation: fade-rotate-2 800ms forwards 200ms;
	}
	&__title {
		font-size: 7.5rem;
		font-weight: 500;
		line-height: 0.89;
		animation: fade-rotate 800ms forwards;
		@media only screen and (max-width: 767px) {
			font-size: min(45px, 6rem);
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
		max-width: 700px;
		&-container {
			display: flex;
			justify-content: center;
		}

		img {
			position: absolute;
			inset: 0;
			width: 100%;
			height: 100%;
			object-fit: cover;
			&:last-child {
				animation: up-down 4s linear infinite alternate;
			}
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
</style>
