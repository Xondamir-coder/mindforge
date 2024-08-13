<template>
	<section class="services section-padding">
		<div class="services__bg"></div>
		<div class="services__head">
			<span class="services__label">Services</span>
			<h1 class="services__title">We offer a variety of services</h1>
		</div>
		<ul class="services__list">
			<li class="services__item" v-for="service in services" :key="service.text">
				<div class="services__icon-container">
					<component class="services__icon" :is="service.icon" />
				</div>
				<h2 class="services__item-title">{{ service.title }}</h2>
				<p class="services__item-text">{{ service.text }}</p>
			</li>
		</ul>
	</section>
</template>

<script setup>
import IconStudy from './icons/IconStudy.vue';

const services = [
	{
		icon: IconStudy,
		title: 'Service Name',
		text: 'Мы преобразуем учебные материалы в интерактивный онлайн формат, делая обучение более увлекательным и понятным.'
	},
	{
		icon: IconStudy,
		title: 'Service Name',
		text: 'Мы разрабатываем учебные пособия, специально адаптированные для онлайн и гибридных форм обучения, чтобы обеспечить эффективное обучение в любой среде.'
	},
	{
		icon: IconStudy,
		title: 'Service Name',
		text: 'Мы создаем интерактивные лекции, которые вдохновляют и учат, делая процесс обучения более интересным и запоминающимся.'
	},
	{
		icon: IconStudy,
		title: 'Service Name',
		text: 'Мы разрабатываем авторские курсы, которые можно легко использовать на сайтах или образовательных платформах, чтобы делиться знаниями с аудиторией.'
	},
	{
		icon: IconStudy,
		title: 'Service Name',
		text: 'Мы автоматизируем процессы обучения и повышения квалификации, облегчая доступ к непрерывному обучению.'
	},
	{
		icon: IconStudy,
		title: 'Service Name',
		text: 'Мы внедряем системы управления обучением (LMS), которые автоматизируют рутинные процессы мониторинга и управления обучением.'
	},
	{
		icon: IconStudy,
		title: 'Service Name',
		text: 'Мы снимаем видеоматериалы для уроков, лекций, семинаров и тренингов, чтобы создать качественный и доступный контент для обучения.'
	}
];
</script>

<style lang="scss" scoped>
.services {
	display: flex;
	flex-direction: column;
	gap: 7rem;
	color: var(--dark-gray);
	position: relative;
	&.active &__head {
		opacity: 1;
		transform: translateY(0);
	}
	&.active &__item {
		transform: scale(1) translate(0, 0);
	}
	&__bg {
		background-color: #fbfbfb;
		position: absolute;
		width: 70%;
		top: 0;
		bottom: 0%;
		z-index: -1;
		left: 50%;
		transform: translateX(-50%);
		@media screen and (max-width: 768px) {
			width: 80%;
		}
	}
	&__head {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 1.5rem;
		text-align: center;
		opacity: 0;
		transform: translateY(5rem);
		transition: transform 500ms, opacity 500ms;
	}
	&__label {
		font-size: 14px;
		font-weight: 600;
		background-color: var(--blue-light);
		color: var(--blue-dark);
		padding: 0.7rem 2rem;
		border-radius: 200px;
	}
	&__title {
		font-size: 3.9rem;
		font-weight: 600;
		line-height: 1.2;
	}
	&__list {
		list-style: none;
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
		gap: 2.5rem;
		justify-content: center;
	}
	&__item {
		background-color: #fff;
		border: 1px solid #e9e9e9;
		border-radius: 15px;
		flex-direction: column;
		align-items: flex-start;
		padding: 35px 24px 30px 40px;
		display: flex;
		box-shadow: 0 2px 12px rgba(15, 15, 15, 0.1);
		gap: 1.5rem;
		transform: scale(0) translate(-100%, -100%);
		transition: transform 700ms;
		&:nth-child(2) {
			transition-delay: 100ms;
		}
		&:nth-child(3) {
			transition-delay: 200ms;
		}
		&:nth-child(4) {
			transition-delay: 300ms;
		}
		&:nth-child(5) {
			transition-delay: 400ms;
		}
		&:nth-child(6) {
			transition-delay: 500ms;
		}
		&:nth-child(7) {
			transition-delay: 600ms;
		}
		&-text {
			font-size: 16px;
			font-weight: 600;
			line-height: 1.4;
		}
		&-title {
			font-size: 2.2rem;
			font-weight: 600;
		}
	}
	&__icon {
		width: 50%;
		height: 50%;
		color: var(--blue-dark);
		&-container {
			width: 8.6rem;
			height: 8.6rem;
			background-color: var(--blue-light);
			border-radius: 50%;
			display: grid;
			place-items: center;
			margin-bottom: 1rem;
		}
	}
}
</style>
