<template>
	<section class="cta section-padding">
		<div class="cta__links">
			<div class="cta__link">
				<IconMail />
				<p>Looking for help? <a href="#">Contact us today</a></p>
			</div>
			<div class="cta__link">
				<IconLike class="cta__icon" />
				<p>Keep in touch. <a href="#">Like us on Facebook</a></p>
			</div>
		</div>
		<div class="cta__banner">
			<h1 class="cta__title">Admission is open for the next year batch</h1>
			<Button label="Get started now" class="cta__button" />
			<a href="tel:+1 800 222 000" class="cta__call">
				<IconCall class="cta__icon" />
				<span>+1 800 222 000</span>
			</a>
		</div>
	</section>
</template>

<script setup>
import Button from './Button.vue';
import IconCall from './icons/IconCall.vue';
import IconLike from './icons/IconLike.vue';
import IconMail from './icons/IconMail.vue';
</script>

<style lang="scss" scoped>
.cta {
	display: flex;
	flex-direction: column;
	gap: 5rem;
	&__call {
		color: var(--dark-gray);
		font-size: 19px;
		font-weight: 600;
		display: flex;
		align-items: center;
		gap: 1rem;
	}
	&__title {
		font-size: 28px;
		font-weight: 600;
		font-family: var(--font-alt);
	}
	&__button {
		background-color: var(--dark-gray);
		color: #fff;
	}
	&__banner {
		background-color: var(--base-color);
		display: flex;
		align-items: center;
		gap: 3rem;
		padding: 3.6rem min(6vw, 6rem);
		border-radius: 8px;
		background-image: url('@/assets/images/cta-bg.webp');
		background-repeat: no-repeat;
		flex-wrap: wrap;
	}
	&__link {
		display: flex;
		align-items: center;
		gap: 1rem;
		color: var(--dark-gray);
		font-weight: 500;
	}
	&__links {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		column-gap: 10rem;
		row-gap: 4rem;
		font-size: 20px;
		a {
			font-weight: bold;
			color: inherit;
		}
	}
	&__icon {
		width: 1.7rem;
		height: 1.7rem;
	}
}
</style>
