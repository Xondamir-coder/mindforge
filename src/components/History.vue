<template>
	<section class="history section-padding" ref="historyRef">
		<div class="history__head">
			<p class="history__label">{{ $t('history-label') }}</p>
			<h1 class="history__title">{{ $t('history-title') }}</h1>
		</div>
		<ul class="history__list">
			<li class="history__item" v-for="content in contents" :key="content.title">
				<div class="history__icon">
					<component :is="content.icon" />
				</div>
				<h2 class="history__item-title">{{ content.title }}</h2>
				<p class="history__item-text">{{ content.text }}</p>
			</li>
		</ul>
	</section>
</template>

<script setup>
import { i18n } from '@/locales';
import { computed } from 'vue';
import IconLessons from './icons/IconLessons.vue';
import IconSubjects from './icons/IconSubjects.vue';
import IconPages from './icons/IconPages.vue';
import IconReading from './icons/IconReading.vue';
import IconDirections from './icons/IconDirections.vue';
import IconUsers from './icons/IconUsers.vue';
import IconVideos from './icons/IconVideos.vue';

const contents = computed(() => [
	{
		icon: IconLessons,
		title: i18n.global.t('history-title-1'),
		text: i18n.global.t('history-text-1'),
		date: i18n.global.t('history-date-1')
	},
	{
		icon: IconSubjects,
		title: i18n.global.t('history-title-2'),
		text: i18n.global.t('history-text-2'),
		date: i18n.global.t('history-date-2')
	},
	{
		icon: IconPages,
		title: i18n.global.t('history-title-3'),
		text: i18n.global.t('history-text-3'),
		date: i18n.global.t('history-date-3')
	},
	{
		icon: IconReading,
		title: i18n.global.t('history-title-4'),
		text: i18n.global.t('history-text-4'),
		date: i18n.global.t('history-date-4')
	},
	{
		icon: IconDirections,
		title: i18n.global.t('history-title-5'),
		text: i18n.global.t('history-text-5'),
		date: i18n.global.t('history-date-5')
	},
	{
		icon: IconLessons,
		title: i18n.global.t('history-title-6'),
		text: i18n.global.t('history-text-6'),
		date: i18n.global.t('history-date-6')
	},
	{
		icon: IconUsers,
		title: i18n.global.t('history-title-7'),
		text: i18n.global.t('history-text-7'),
		date: i18n.global.t('history-date-7')
	},
	{
		icon: IconVideos,
		title: i18n.global.t('history-title-8'),
		text: i18n.global.t('history-text-8'),
		date: i18n.global.t('history-date-8')
	}
]);
</script>

<style lang="scss" scoped>
.history {
	display: flex;
	flex-direction: column;
	gap: 6rem;
	color: var(--dark-gray);
	overflow: hidden;
	&.active &__head {
		opacity: 1;
		transform: rotateY(0) translate(0, 0);
	}
	&.active &__list {
		transform: perspective(800px) rotateX(0) translateZ(0);
	}
	&__icon {
		width: 10rem;
		height: 10rem;
		background-color: rgba(247, 247, 247, 0.97);
		border-radius: 50%;
		margin-bottom: 3rem;
		display: grid;
		place-items: center;
		transition: background-color 400ms;
		svg {
			transform: translateY(3rem);
			fill: black;
			width: 85%;
			height: 85%;
			z-index: 10;
			position: relative;
			transition: fill 400ms;
		}
	}
	&__list {
		list-style: none;
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		row-gap: 4rem;
		transform-style: preserve-3d;
		transform: perspective(800px) rotateX(33deg) translateZ(75px);
		transition: transform 1.5s;
	}
	&__item {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 10px;
		padding: 25%;
		border: 1px solid var(--extra-medium-gray);
		position: relative;
		transition: background-color 400ms, color 400ms;
		&:hover {
			background-color: var(--dark-gray);
			color: #fff;
			svg {
				fill: #fff;
			}
			.history__icon {
				background-color: var(--dark-gray);
			}
		}
		&-title {
			font-size: 18px;
		}
		&-text {
			font-size: 16px;
		}
	}
	&__head {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 1.5rem;
		text-align: center;
		color: var(--dark-gray);
	}
	&__title {
		font-size: 4.8rem;
		font-weight: 700;
	}
	&__label {
		font-size: 16px;
		font-weight: 600;
	}
}
</style>
