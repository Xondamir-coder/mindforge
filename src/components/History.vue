<template>
	<section class="history section-padding" ref="historyRef">
		<div class="history__head">
			<p class="history__label">Our story</p>
			<h1 class="history__title">Delivering 6 years of excellence</h1>
			<p class="history__text">
				Mindforge is a young and dynamic owner driven Destination Management Company that
				opened its doors to the world of tourism in 2010. Along with passion, commitment and
				discipline, our well-knit team converts its profound knowledge into memorable
				experiences for every guest.
			</p>
		</div>
		<div class="history__content">
			<div class="history__bar"></div>
			<div class="history__box" v-for="content in history" :key="content.date">
				<div class="history__box-left">
					<h2 class="history__box-title">{{ content.date }}</h2>
					<h3 class="history__box-subtitle">{{ content.title }}</h3>
				</div>
				<div class="history__box-middle">
					<div class="history__circle"></div>
				</div>
				<div class="history__box-right">
					<p class="history__box-desc">{{ content.desc }}</p>
				</div>
			</div>
		</div>
	</section>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const history = [
	{
		date: 'Jan 2010',
		title: 'Opened its doors to the world of tourism',
		desc: 'Mindforge opened its doors to the world of tourism in 2010. Its passion, dedication, and discipline have allowed it to grow into a dynamic and successful Destination Management Company.'
	},
	{
		date: 'Jan 2011',
		title: 'Stabilized the business and gained confidence',
		desc: 'With a solid foundation, Mindforge gained confidence and stability in its business operations. It continued to refine its services and expand its reach.'
	},
	{
		date: 'Jan 2012',
		title: 'Increased the number of tours and tourists',
		desc: 'Mindforge successfully increased the number of tours and tourists, cementing its position as a reliable and trustworthy partner in the tourism industry.'
	},
	{
		date: 'Jan 2013',
		title: 'Strengthened the brand and attracted customers',
		desc: 'The brand was further strengthened, making Mindforge a name synonymous with quality and excellence in the tourism industry. It attracted more customers and built a loyal customer base.'
	},
	{
		date: 'Jan 2014',
		title: 'Introduced new services and products',
		desc: 'Mindforge continued to innovate and introduce new services and products. It expanded its offerings and provided a wider range of experiences for its customers.'
	}
];
const historyRef = ref();

onMounted(() => {
	const handler = entries => {
		entries.forEach(entry => {
			console.log(entry.isIntersecting);
			if (entry.isIntersecting) {
				entry.target.classList.add('active');
			} else {
				entry.target.classList.remove('active');
			}
		});
	};
	const observer = new IntersectionObserver(handler, { threshold: 0.9 });
	historyRef.value.querySelectorAll('.history__box').forEach(box => observer.observe(box));
});
</script>

<style lang="scss" scoped>
.history {
	display: flex;
	flex-direction: column;
	gap: max(8rem, 10vw);
	color: var(--dark-gray);
	&.active &__head {
		opacity: 1;
		transform: rotateY(0) translate(0, 0);
	}
	&__box {
		font-weight: 700;
		display: grid;
		align-self: start;
		grid-template-columns: 1fr 19.2rem 1fr;
		height: 100%;
		grid-template-areas: 'left middle right';
		@media only screen and (max-width: 800px) {
			grid-template-columns: initial;
			gap: 4rem;
			grid-template-areas:
				'middle left'
				'middle right';
		}
		& > *:not(.history__box-middle) {
			transition: opacity 600ms;
			opacity: 0.5;
		}
		&.active > * {
			opacity: 1;
		}
		&.active .history__circle {
			box-shadow: 0 0 0 8px var(--dark-gray);
		}
		&-right {
			grid-area: right;
		}
		&-left {
			display: flex;
			flex-direction: column;
			gap: 1rem;
			grid-area: left;
		}
		&-middle {
			grid-area: middle;
			display: grid;
			justify-items: center;
		}
		&-title {
			font-size: 4rem;
		}
		&-subtitle {
			font-size: 3.2rem;
		}
		&-desc {
			font-size: 18px;
			font-weight: 400;
			letter-spacing: 0.2px;
			line-height: 1.7;
		}
	}
	&__content {
		position: relative;
		display: grid;
		place-items: center;
		grid-auto-rows: 20rem;
		gap: 5vw;
		@media only screen and (max-width: 800px) {
			grid-auto-rows: 1fr;
			gap: 10rem;
		}
	}
	&__circle {
		border-radius: 100%;
		width: 1.5rem;
		height: 1.5rem;
		position: sticky;
		top: 50vh;
		box-shadow: 0 0 0 8px #a4b4af;
		background-color: #fff;
		transition: box-shadow 600ms;
	}
	&__bar {
		background-color: var(--dark-gray);
		height: 100%;
		width: 3px;
		position: absolute;
		@media only screen and (max-width: 800px) {
			justify-self: flex-start;
			left: 5px;
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
	&__text {
		font-size: 18px;
		max-width: 60ch;
		line-height: 27px;
		text-align: center;
		letter-spacing: 0.2px;
	}
}
</style>
