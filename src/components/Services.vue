<template>
	<section class="services section-padding">
		<div class="services__bg"></div>
		<div class="services__head">
			<span class="services__label">{{ $t('services-label') }}</span>
			<h1 class="services__title">
				{{ $t('services-title') }}
			</h1>
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
import IconAdaptation from './icons/IconAdaptation.vue';
import IconStudy from './icons/IconStudy.vue';
import IconInteractive from './icons/IconInteractive.vue';
import IconAuthor from './icons/IconAuthor.vue';
import IconAutomation from './icons/IconAutomation.vue';
import IconSystem from './icons/IconSystem.vue';
import IconVideo from './icons/IconVideo.vue';
import { computed } from 'vue';
import { i18n } from '@/locales';

const services = computed(() => [
	{
		icon: IconStudy,
		title: i18n.global.t('services-title-1'),
		text: i18n.global.t('services-text-1')
	},
	{
		icon: IconAdaptation,
		title: i18n.global.t('services-title-2'),
		text: i18n.global.t('services-text-2')
	},
	{
		icon: IconInteractive,
		title: i18n.global.t('services-title-3'),
		text: i18n.global.t('services-text-3')
	},
	{
		icon: IconAuthor,
		title: i18n.global.t('services-title-4'),
		text: i18n.global.t('services-text-4')
	},
	{
		icon: IconAutomation,
		title: i18n.global.t('services-title-5'),
		text: i18n.global.t('services-text-5')
	},
	{
		icon: IconSystem,
		title: i18n.global.t('services-title-6'),
		text: i18n.global.t('services-text-6')
	},
	{
		icon: IconVideo,
		title: i18n.global.t('services-title-7'),
		text: i18n.global.t('services-text-7')
	}
]);
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
		font-size: 16px;
		font-weight: 600;
	}
	&__title {
		font-size: 3.9rem;
		font-weight: 600;
		line-height: 1.2;
		max-width: 30ch;
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
			border: 2px solid #0d3858;
			border-radius: 50%;
			display: grid;
			place-items: center;
			margin-bottom: 1rem;
			box-shadow: 0px 0px 5px 0px #0d3858 inset;
		}
	}
}
</style>
