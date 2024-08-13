<template>
	<section class="product section-padding">
		<div class="product__head">
			<span class="product__label">Продукт</span>
			<h1 class="product__title">Мы предлагаем продукт</h1>
		</div>
		<div class="product__images">
			<img
				v-for="(image, index) in images"
				:key="index"
				:style="{ transform: `translateX(${(index - curSlide) * 100}%)` }"
				class="product__image"
				:src="image"
				alt="product img" />
			<button v-if="images.length > 1" class="product__button" @click="changeSlide('prev')">
				<IconLess class="product__button-icon" />
			</button>
			<button v-if="images.length > 1" class="product__button" @click="changeSlide('next')">
				<IconGreater class="product__button-icon" />
			</button>
			<ul class="product__nav">
				<li class="product__nav-item" v-for="i in [0]" :key="i">
					<button
						class="product__nav-button"
						:class="{ active: curSlide === i }"
						@click="curSlide = i"></button>
				</li>
			</ul>
		</div>
		<div class="product__content">
			<div class="product__box" v-for="(content, i) in contents" :key="content.title">
				<p class="product__box-desc">{{ content.title }}:</p>
				<p class="product__box-desc">{{ content.desc }}</p>
			</div>
		</div>
	</section>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue';
import IconGreater from './icons/IconGreater.vue';
import IconLess from './icons/IconLess.vue';
import imgUrl1 from '@/assets/images/product-1.avif';
// import imgUrl2 from '@/assets/images/product-2.webp';
// import imgUrl3 from '@/assets/images/product-3.webp';

const curSlide = ref(0);
// const images = [imgUrl1, imgUrl2, imgUrl3];
const images = [imgUrl1];
const contents = [
	{
		title: 'Edulab',
		desc: 'Система управления обучением для различных организаций в Узбекистане, автоматизирующая процесс обучения и повышающая административную эффективность на единой централизованной платформе.'
	}
];

const changeSlide = direction => {
	if (direction === 'next') {
		curSlide.value = curSlide.value === images.length - 1 ? 0 : curSlide.value + 1;
	} else {
		curSlide.value = curSlide.value === 0 ? images.length - 1 : curSlide.value - 1;
	}
};

onMounted(() => {
	document.addEventListener('keyup', e => {
		if (e.key === 'ArrowRight') {
			changeSlide('next');
		} else if (e.key === 'ArrowLeft') {
			changeSlide('prev');
		}
	});
});
onUnmounted(() => {
	document.removeEventListener('keyup');
});
</script>

<style lang="scss" scoped>
.product {
	display: flex;
	flex-direction: column;
	gap: 3rem;
	color: var(--dark-gray);
	&__box {
		display: flex;
		flex-direction: column;
		gap: 1rem;
	}
	&.active &__box {
		opacity: 1;
		transform: rotateY(0) translate(0, 0);
	}
	&.active &__images {
		transform: scale(1);
	}
	&__content {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		row-gap: 5rem;
	}
	&__box {
		opacity: 0;
		transform: rotateY(-100deg) translate(9rem, 9rem);
		transition: opacity 600ms, transform 600ms;
		&:nth-of-type(2) {
			transition-delay: 200ms;
		}
		&:nth-of-type(3) {
			transition-delay: 400ms;
		}
		&-desc {
			font-size: 2.4rem;
			line-height: 1.4;
			font-weight: 700;
			letter-spacing: -0.5px;
			&:last-of-type {
				opacity: 0.7;
			}
		}
	}
	&__nav {
		list-style: none;
		position: absolute;
		bottom: 15px;
		left: 50%;
		transform: translateX(-50%);
		display: flex;
		gap: 10px;
		&-button {
			background-color: transparent;
			border: none;
			border-radius: 50%;
			background-color: rgba(255, 255, 255, 0.4);
			z-index: 2;
			width: 12px;
			height: 12px;
			transition: background-color 300ms;
			&.active {
				background-color: #fff;
			}
		}
	}
	&__button {
		position: absolute;
		background-color: transparent;
		border: none;
		background-color: var(--blue-very-light);
		width: 6.5rem;
		height: 6.5rem;
		border-radius: 13px;
		cursor: pointer;
		top: 50%;
		transform: translateY(-50%);

		&:first-of-type {
			left: 2vw;
			&:hover {
				.product__button-icon {
					transform: translateX(-7px);
				}
			}
		}
		&:last-of-type {
			right: 2vw;
			&:hover {
				.product__button-icon {
					transform: translateX(7px);
				}
			}
		}
		&-icon {
			fill: var(--blue);
			width: 40%;
			height: 40%;
			transition: transform 300ms;
		}
	}
	&__images {
		position: relative;
		height: max(50vw, 280px);
		overflow: hidden;
		transform: scale(0);
		transition: transform 1s;
	}
	&__image {
		border-radius: 20px;
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		object-fit: cover;
		transition: transform 1s;
	}
	&.active &__head {
		opacity: 1;
		transform: translateY(0);
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
}
</style>
