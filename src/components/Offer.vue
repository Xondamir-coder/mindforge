<template>
	<section class="offer section-padding">
		<div class="offer__lines"></div>
		<img ref="objRef" class="offer__obj" src="@/assets/images/offer-obj.png" alt="offer obj" />
		<div class="offer__left">
			<div class="offer__top">
				<div class="offer__icon-container">
					<IconChat class="offer__icon" />
				</div>
				<span>Мы делаем для всех</span>
			</div>
			<h1 class="offer__title">Наши предложения для_</h1>
			<p class="offer__text">
				Создавайте и монетизируйте онлайн-курсы с возможностью контроля обучения и повышения
				квалификации
			</p>
			<div class="offer__content">
				<h2 class="offer__content-data">99%</h2>
				<div class="offer__content-divider"></div>
				<div class="offer__content-text">Клиенты успешно завершают курсы</div>
			</div>
		</div>
		<div class="offer__right">
			<button class="offer__button" @click="changeCurSlide('prev')">
				<IconLess class="offer__button-icon" />
			</button>
			<button class="offer__button" @click="changeCurSlide('next')">
				<IconGreater class="offer__button-icon" />
			</button>
			<div class="offer__container">
				<div
					class="offer__box"
					v-for="(content, index) in contents"
					:key="content.name"
					:style="{
						transform: `translateX(calc(${(index - curSlide) * 100}% + ${
							(index - curSlide) * 50
						}px))`
					}">
					<img class="offer__box-img" :src="content.img" alt="img" />
					<div class="offer__box-content">
						<h3 class="offer__box-name">_{{ content.for }}</h3>
						<p class="offer__box-text">{{ content.text }}</p>
					</div>
				</div>
			</div>
		</div>
	</section>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import IconChat from './icons/IconChat.vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);
import offerImg1 from '@/assets/images/offer-1.webp';
import offerImg2 from '@/assets/images/offer-2.webp';
import offerImg3 from '@/assets/images/offer-3.webp';
import offerImg4 from '@/assets/images/offer-4.webp';
import offerImg5 from '@/assets/images/offer-5.webp';
import IconLess from './icons/IconLess.vue';
import IconGreater from './icons/IconGreater.vue';

const objRef = ref();
const curSlide = ref(0);
const contents = [
	{
		img: offerImg1,
		text: 'Онлайн-тренинги для подготовки и повышения квалификации персонала, а также LMS для мониторинга и контроля обучения сотрудников',
		for: 'Корпоративных клиентов'
	},
	{
		img: offerImg2,
		text: 'Разработка онлайн-курсов по авторским программам с возможностью размещения и монетизации собственных курсов на платформе для широкой аудитории',
		for: 'Независимых авторов курсов:'
	},
	{
		img: offerImg3,
		for: 'Школ',
		text: 'Онлайн-уроки по школьной программе и авторским курсам, курсы по профессиональным навыкам и подготовке к экзаменам, а также система управления обучением (LMS) для эффективного ведения учебного процесса'
	},
	{
		img: offerImg4,
		for: 'Университетов',
		text: 'Онлайн-уроки для дистанционного и гибридного обучения по авторским программам, тесты и экзамены для оценки знаний, дополнительные курсы по профессиональным навыкам, а также LMS для управления образовательным процессом'
	},
	{
		img: offerImg5,
		for: 'Учебных центров',
		text: 'Онлайн-уроки по авторским программам для дистанционного и гибридного обучения, задания для самостоятельной работы и проверки знаний, а также LMS для эффективного управления процессом обучения'
	}
];

const changeCurSlide = direction => {
	if (direction === 'next') {
		curSlide.value = curSlide.value === contents.length - 1 ? 0 : curSlide.value + 1;
	} else {
		curSlide.value = curSlide.value === 0 ? contents.length - 1 : curSlide.value - 1;
	}
};

onMounted(() => {
	gsap.to(objRef.value, {
		y: 200,
		scrollTrigger: {
			trigger: '.offer',
			scrub: 1,
			start: '-=50'
		}
	});

	// setInterval(() => {
	// 	changeCurSlide('next');
	// }, 8000);
});
</script>

<style lang="scss" scoped>
.offer {
	color: #fff;
	background-image: linear-gradient(to right bottom, #154c79, #0f3757, #0d2c43, #0b1e31, #091227);
	position: relative;
	display: grid;
	grid-auto-columns: 1fr 1.5fr;
	grid-template-areas: 'left right';
	gap: 10rem;
	overflow: hidden;
	padding-top: 15rem;
	padding-bottom: 15rem;

	&.active &__left > *:not(.offer__text) {
		opacity: 1;
		transform: rotateY(0) translate(0, 0);
	}
	&.active &__text {
		opacity: 0.4;
		transform: rotateY(0) translate(0, 0);
	}
	&.active &__button {
		scale: 1;
	}
	@media only screen and (max-width: 1300px) {
		grid-auto-columns: initial;
		grid-template-areas:
			'left'
			'right';
	}
	&__container {
		overflow: hidden;
		width: 100%;
		position: relative;
		@media only screen and (max-width: 1300px) {
			min-height: 50vh;
		}
		@media only screen and (max-width: 900px) {
			min-height: 100vh;
		}
		@media only screen and (max-width: 600px) {
			min-height: 110vh;
		}
	}
	&__left {
		grid-area: left;
		position: relative;
		z-index: 1;
		display: flex;
		flex-direction: column;
		gap: 30px;
		font-family: var(--font-alt);
		& > * {
			opacity: 0;
			transform: rotateY(-100deg) translate(9rem, 9rem);
			transition: opacity 800ms, transform 800ms;
		}
	}
	&__right {
		grid-area: right;
		position: relative;
		z-index: 1;
		display: flex;
	}
	&__button {
		border: none;
		background-color: transparent;
		width: 4.5rem;
		height: 4.5rem;
		position: absolute;
		z-index: 2;
		border-radius: 50%;
		display: grid;
		place-items: center;
		background-color: #fff;
		top: 50%;
		transform: translate(-50%, -50%);
		box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
		scale: 0;
		transition: scale 300ms;
		transition-delay: 0.5s;
		&:first-of-type {
			left: 0;
			&:hover .offer__button-icon {
				transform: translateX(-5px);
			}
		}
		&:last-of-type {
			left: 100%;
			transition-delay: 0.8s;
			&:hover .offer__button-icon {
				transform: translateX(5px);
			}
		}

		&-icon {
			fill: var(--dark-gray);
			width: 50%;
			height: 50%;
			transition: transform 300ms;
		}
	}
	&__box {
		position: absolute;
		inset: 0;
		color: var(--medium-gray);
		background-color: #fff;
		border-radius: 10px;
		transition: transform 1s;
		display: grid;
		grid-template-columns: 1fr 1.5fr;
		@media only screen and (max-width: 900px) {
			grid-template-columns: initial;
			grid-template-rows: 40rem 1fr;
		}
		&-img {
			object-fit: cover;
			border-top-left-radius: 10px;
			border-bottom-left-radius: 10px;
			height: 100%;
			width: 100%;
		}
		&-text {
			line-height: 30px;
			font-size: 17px;
		}
		&-name {
			font-size: 18px;
			font-weight: 600;
			color: var(--dark-gray);
		}
		&-content {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: start;
			gap: 2rem;
			padding: 6rem;
			@media only screen and (max-width: 900px) {
				padding: 3rem;
			}
		}
	}
	&__stars {
		padding: 1rem 2rem;
		display: flex;
		justify-content: start;
		gap: 3px;
		background-color: #ef991f;
		border-radius: 50px;
	}
	&__content {
		display: flex;
		gap: 4rem;
		transition-delay: 600ms;
		&-divider {
			width: 1px;
			background-color: rgba(255, 255, 255, 0.2);
		}
		&-data {
			font-size: 5.5rem;
			font-weight: 600;
		}
		&-text {
			align-self: center;
			line-height: 26px;
		}
	}
	&__text {
		font-size: 17px;
		max-width: 80%;
		font-family: var(--font-base);
		line-height: 1.8;
		transition-delay: 400ms;
	}
	&__title {
		font-size: 5.5rem;
		line-height: 0.85;
		font-family: var(--font-alt);
		letter-spacing: -3px;
		font-weight: 600;
		transition-delay: 200ms;
	}

	&__obj {
		position: absolute;
		left: -10rem;
		top: 2rem;
	}
	&__lines {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-image: url('@/assets/images/hero-lines.svg');
		background-size: 13.5rem;
	}
	&__top {
		display: flex;
		align-items: center;
		gap: 10px;
		font-size: 1.9rem;
		font-weight: 500;
	}
	&__icon {
		width: 2.2rem;
		height: 2.2rem;
		color: var(--dark-gray);
		&-container {
			display: grid;
			place-items: center;
			background-color: var(--base-color);
			border-radius: 50%;
			width: 5.5rem;
			height: 5.5rem;
		}
	}
}
</style>
