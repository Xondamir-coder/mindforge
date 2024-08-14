<template>
	<section class="skills">
		<div
			ref="imgContainerRef"
			class="skills__images"
			@mousemove="handleMouseMove"
			@mouseleave="handleMouseLeave">
			<img class="skills__image" src="@/assets/images/girl.webp" alt="девочка" />
			<img class="skills__image" src="@/assets/images/blue-object.webp" alt="синяя вещь" />
		</div>
		<div class="skills__main">
			<div class="skills__head">
				<div class="skills__icon-container">
					<IconBriefcase class="skills__icon" />
				</div>
				<p>Премиальное обучение</p>
			</div>
			<h1 class="skills__title">Что мы предлагаем</h1>
			<div class="skills__content">
				<div
					class="skills__box"
					v-for="(skill, i) in skills"
					:key="i"
					:class="{ active: activeItem === i }"
					@click="activeItem = i">
					<h2 class="skills__box-title">{{ skill.title }}</h2>
					<div class="skills__box-box">
						<p class="skills__box-text">{{ skill.desc }}</p>
						<component class="skills__box-icon" :is="skill.icon" />
					</div>
				</div>
			</div>
		</div>
	</section>
</template>

<script setup>
import { ref } from 'vue';
import IconBook from './icons/IconBook.vue';
import IconBriefcase from './icons/IconBriefcase.vue';
import gsap from 'gsap';

const activeItem = ref(0);
const imgContainerRef = ref();

const skills = [
	{
		title: 'Для школ',
		desc: 'Онлайн-уроки по школьной программе и авторским курсам, курсы по профессиональным навыкам и подготовке к экзаменам, а также система управления обучением (LMS) для эффективного ведения учебного процесса',
		icon: IconBook
	},
	{
		title: 'Для университетов',
		desc: 'Онлайн-уроки для дистанционного и гибридного обучения по авторским программам, тесты и экзамены для оценки знаний, дополнительные курсы по профессиональным навыкам, а также LMS для управления образовательным процессом',
		icon: IconBook
	},
	{
		title: 'Для учебных центров',
		desc: 'Онлайн-уроки по авторским программам для дистанционного и гибридного обучения, задания для самостоятельной работы и проверки знаний, а также LMS для эффективного управления процессом обучения',
		icon: IconBook
	}
];

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
.skills {
	display: grid;
	grid-template-areas: 'images content';
	grid-auto-columns: 1fr;
	gap: 2rem;
	padding: 10rem 0;
	@media only screen and (max-width: 900px) {
		grid-template-areas:
			'content'
			'images';
	}
	&.active &__main > * {
		opacity: 1;
		transform: rotateY(0) translate(0, 0);
	}
	&__images {
		grid-area: images;
		position: relative;
	}
	&__image {
		width: 100%;
		height: 100%;
		object-fit: contain;
		&:last-of-type {
			position: absolute;
			left: 0;
		}
	}
	&__icon {
		width: 40%;
		height: 40%;
		color: var(--dark-gray);
		&-container {
			display: flex;
			align-items: center;
			justify-content: center;
			width: 5.5rem;
			height: 5.5rem;
			border-radius: 50%;
			background-color: var(--base-color);
		}
	}
	&__main {
		padding: 0 4vw;
		padding-right: 7vw;
		max-width: 700px;
		grid-area: content;
		display: flex;
		flex-direction: column;
		gap: 20px;
		& > * {
			opacity: 0;
			transform: rotateY(-100deg) translate(9rem, 9rem);
			transition: opacity 800ms, transform 800ms;
		}
		@media only screen and (max-width: 900px) {
			max-width: 100%;
		}
	}
	&__content {
		display: flex;
		flex-direction: column;
		// gap: 1rem;
		margin-top: 3rem;
		transition-delay: 400ms;
	}
	&__head {
		display: flex;
		align-items: center;
		gap: 15px;
		font-size: 1.9rem;
		font-weight: 500;
		font-family: var(--font-alt);
	}
	&__title {
		font-size: 5.5rem;
		line-height: 0.85;
		font-family: var(--font-alt);
		letter-spacing: -3px;
		font-weight: 600;
		transition-delay: 200ms;
	}
	&__box {
		cursor: pointer;
		padding: 1.5rem min(5vw, 5rem);
		border-radius: 4px;
		display: flex;
		flex-direction: column;
		gap: 1.5rem;
		position: relative;
		overflow: hidden;
		&.active {
			background-image: linear-gradient(to bottom, #f2f8f7, #f5fafa, #f9fbfd, #fcfdfe, #fff);
		}
		&.active &-icon {
			opacity: 0.15;
			translate: 0 0;
		}
		&.active &-box {
			max-height: 100rem;
		}
		&-box {
			width: 100%;
			align-items: center;
			display: flex;
			justify-content: space-between;
			max-width: 30rem;
			max-height: 0;
			overflow: hidden;
			transition: max-height 1s;
		}
		&-title {
			font-size: 18px;
			font-weight: 600;
		}
		&-text {
			font-size: 17px;
			line-height: 1.5;
			color: rgb(130, 140, 138);
		}
		&-icon {
			position: absolute;
			width: 9rem;
			height: 9rem;
			opacity: 0;
			right: -20px;
			transform: rotate(-35deg);
			translate: 0 -5rem;
			transition: opacity 800ms, translate 800ms;
		}
	}
}
</style>
