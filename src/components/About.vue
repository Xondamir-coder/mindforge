<template>
	<div class="container">
		<button class="scroll" @click="scrollToAbout">
			<IconMouse />
		</button>
		<section ref="aboutRef" class="about section-padding">
			<img
				ref="imgRef"
				class="about__ellipse"
				src="@/assets/images/about-ellipse.webp"
				alt="ellipse" />
			<div class="about__left">
				<div class="about__head">
					<div class="about__top">
						<div class="about__icon-container">
							<IconAward class="about__icon" />
						</div>
						<span>Гарантируем и сертифицируем</span>
					</div>
					<h1 class="about__title">Учитесь онлайн в удобное время</h1>
					<button class="about__button">Узнать больше <span>&rightarrow;</span></button>
				</div>
				<div class="about__experts">
					<img src="@/assets/images/random-ppl.webp" alt="randos" />
					<p>Онлайн-курсы от <a class="about__link" href="#">экспертов.</a></p>
				</div>
			</div>
			<div class="about__right">
				<div class="about__box" v-for="(content, index) in contents" :key="index">
					<div class="about__box-num">0{{ index + 1 }}</div>
					<h2 class="about__box-title">
						{{ content.title }}
					</h2>
					<p class="about__box-text">
						{{ content.text }}
					</p>
					<div class="about__box-divider"></div>
				</div>
			</div>
		</section>
	</div>
</template>

<script setup>
import lenis from '@/js/lenis';
import { onMounted, ref } from 'vue';
import IconAward from './icons/IconAward.vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import IconMouse from './icons/IconMouse.vue';
gsap.registerPlugin(ScrollTrigger);

const contents = [
	{
		title: 'Гибкий график',
		text: 'Онлайн-обучение позволяет учащимся проходить курсы в удобное время, ускоряя процесс усвоения материала.'
	},
	{
		title: 'Доступная стоимость',
		text: 'Онлайн-обучение позволяет значительно сократить затраты на обучение без потери качества контента.'
	},
	{
		title: 'Экспертные преподаватели',
		text: 'Наши курсы разрабатываются профессионалами, чтобы обеспечить высокое качество и актуальность материалов.'
	}
];

const imgRef = ref();
const aboutRef = ref();

const scrollToAbout = () => {
	lenis.scrollTo(aboutRef.value, {
		duration: 2.5
	});
};

onMounted(() => {
	gsap.to(imgRef.value, {
		y: -200,
		scrollTrigger: {
			trigger: '.about',
			start: 'top top',
			scrub: 1
		}
	});
});
</script>

<style lang="scss" scoped>
.scroll {
	cursor: pointer;
	position: absolute;
	left: 50%;
	transform: translateX(-50%);
	top: -3.5rem;
	width: 7rem;
	height: 7rem;
	background-color: #fff;
	border-radius: 50%;
	border: none;
	box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
}
.about {
	background-image: url('@/assets/images/about-bg.png');
	background-repeat: no-repeat;
	display: grid;
	grid-template-areas: 'left right';
	grid-auto-columns: 1fr;
	gap: 15vw;
	color: var(--dark-gray);
	overflow: hidden;

	@media only screen and (max-width: 768px) {
		grid-template-areas:
			'left'
			'right';
	}
	&.active {
		.about__box {
			opacity: 1;
			transform: translate(0, 0);
		}
		.about__head > * {
			opacity: 1;
			transform: rotateY(0) translate(0, 0);
		}
		.about__experts {
			opacity: 1;
			transform: rotateY(0) translate(0, 0);
		}
	}
	&__top {
		display: flex;
		align-items: center;
		gap: 10px;
		font-size: 1.9rem;
		font-weight: 500;
	}
	&__title {
		font-size: 5.5rem;
		line-height: 0.85;
	}
	&__head {
		display: flex;
		flex-direction: column;
		gap: 3rem;
		align-items: flex-start;
		overflow: hidden;

		& > * {
			opacity: 0;
			transform: rotateY(-90deg) translate(9rem, 9rem);
			transition: transform 600ms, opacity 600ms;
			&:nth-child(2) {
				transition-delay: 150ms;
			}
			&:nth-child(3) {
				transition-delay: 300ms;
			}
		}
		@media only screen and (max-width: 768px) {
			align-items: center;
			text-align: center;
		}
	}
	&__button {
		cursor: pointer;
		background: transparent;
		border: none;
		color: #fff;
		background-color: var(--dark-gray);
		padding: 1.7rem 3rem;
		border-radius: 20px;
		display: flex;
		gap: 1rem;
		transition: transform 300ms, box-shadow 300ms;
		span {
			transition: transform 300ms;
		}

		&:hover {
			transform: translateY(-5px);
			box-shadow: 0 10px 20px rgba(0, 0, 0, 0.45);
			& span {
				transform: translateX(7px);
			}
		}
		&:active {
			transform: translateY(-3px);
			box-shadow: 0 10px 20px rgba(0, 0, 0, 0.35);
		}
	}
	&__left {
		display: flex;
		flex-direction: column;
		grid-area: left;
		gap: 8rem;

		@media only screen and (max-width: 768px) {
			gap: 3rem;
		}
	}
	&__right {
		grid-area: right;
		display: flex;
		flex-direction: column;
		justify-content: center;
		gap: 5rem;

		@media only screen and (max-width: 768px) {
			padding: 0 2rem;
			gap: 10rem;
		}
	}
	&__box {
		position: relative;
		display: flex;
		flex-direction: column;
		gap: 17px;
		opacity: 0;
		transform: translate(50px, 50px);
		transition: transform 600ms, opacity 600ms;
		&:nth-child(3) {
			transition-delay: 300ms;
		}
		&:nth-child(2) {
			align-items: flex-end;
			text-align: right;
			transition-delay: 150ms;
			@media only screen and (max-width: 768px) {
				align-items: flex-start;
			}
			.about__box-num {
				top: -7rem;
				right: -4rem;
				@media only screen and (max-width: 768px) {
					right: initial;
				}
			}
		}
		&-divider {
			height: 1px;
			border-top: 3px solid var(--base-color);
			width: 20%;
		}
		&-num {
			font-family: var(--font-alt);
			opacity: 0.1;
			font-size: 10rem;
			font-weight: 700;
			position: absolute;
			top: -7rem;
			left: -4rem;
		}
		&-title {
			font-size: 20px;
			font-weight: 600;
			max-width: 220px;
		}
		&-text {
			font-size: 17px;
			color: var(--medium-gray);
			max-width: 300px;
			line-height: 1.5;

			@media only screen and (max-width: 768px) {
				max-width: initial;
				text-align: left;
			}
		}
	}
	&__icon {
		width: 2.2rem;
		height: 2.2rem;
		&-container {
			display: grid;
			place-items: center;
			background-color: var(--base-color);
			border-radius: 50%;
			width: 5.5rem;
			height: 5.5rem;
		}
	}

	&__experts {
		font-family: var(--font-base);
		display: flex;
		align-items: center;
		font-size: 17px;
		font-weight: 500;
		opacity: 0;
		transform: rotateY(-90deg) translate(9rem, 9rem);
		transition: transform 600ms, opacity 600ms;
		transition-delay: 450ms;
		overflow: hidden;

		a {
			color: inherit;
			font-weight: bold;
		}
	}
	&__left {
		font-family: var(--font-alt);
		color: var(--dark-gray);
	}
	&__ellipse {
		position: absolute;
		z-index: -1;
		top: 0;
		right: 0;
		width: 30rem;
		height: 50rem;
		@media only screen and (max-width: 800px) {
			top: 50%;
		}
	}
}
.container {
	position: relative;
}
</style>
