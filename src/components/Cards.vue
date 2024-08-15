<template>
	<button @click="changeSlide('prev')" class="cards__button">
		<IconLess class="cards__button-icon" />
	</button>
	<button @click="changeSlide('next')" class="cards__button">
		<IconGreater class="cards__button-icon" />
	</button>
	<div class="cards" ref="cardsRef">
		<div class="card" v-for="content in contents" :key="content.name">
			<div class="card__container">
				<img class="card__img" :src="content.img" alt="img" />
			</div>
			<div class="card__content">
				<h3 class="card__name">_{{ content.for }}</h3>
				<p class="card__text">{{ content.text }}</p>
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref } from 'vue';
import IconLess from './icons/IconLess.vue';
import IconGreater from './icons/IconGreater.vue';

const props = defineProps({
	contents: Array
});

const cardsRef = ref(null);
const currentIndex = ref(0);

const changeSlide = direction => {
	if (direction === 'next') {
		currentIndex.value = Math.min(currentIndex.value + 1, props.contents.length - 1);
	}
	if (direction === 'prev') {
		currentIndex.value = Math.max(currentIndex.value - 1, 0);
	}

	const cardWidth =
		cardsRef.value?.children[0]?.offsetWidth + parseInt(getComputedStyle(cardsRef.value).gap);
	if (cardsRef.value) {
		cardsRef.value.scrollTo({
			left: currentIndex.value * cardWidth,
			behavior: 'smooth'
		});
	}
};
</script>

<style lang="scss" scoped>
.card {
	display: grid;
	grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
	align-items: center;
	// max-width: 50vw;
	row-gap: 5rem;
	min-width: 100%;
	scroll-snap-align: center;
	scroll-behavior: smooth; /* This helps smooth scrolling in general */
	background-color: #fff;
	color: var(--dark-gray);
	border-radius: 10px;
	overflow: hidden;
	&__container {
		flex-basis: 40%;
		align-self: stretch;
	}
	&__img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}
	&__content {
		flex-basis: 50%;
		display: flex;
		flex-direction: column;
		gap: 2rem;
		line-height: 1.5;
		padding: 0 4rem;
		padding-bottom: 4rem;
	}
}

.cards {
	display: flex;
	gap: 5rem;
	overflow-x: scroll;
	scroll-snap-type: x mandatory;
	height: 100%;
	width: 100%;
	&::-webkit-scrollbar {
		display: none;
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
		&:first-of-type {
			left: 0;
			&:hover .cards__button-icon {
				transform: translateX(-5px);
			}
		}
		&:last-of-type {
			left: 100%;
			&:hover .cards__button-icon {
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
}
</style>
