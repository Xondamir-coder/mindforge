<template>
	<section class="section">
		<footer class="footer section-padding">
			<div class="footer__lines"></div>
			<img class="footer__obj" src="@/assets/images/offer-obj.png" />
			<div class="footer__banner">
				<h1 class="footer__banner-title">Admission is open for the next year batch</h1>
				<Button label="Get started now" class="footer__banner-button" />
				<a href="tel:+1 800 222 000" class="footer__banner-call">
					<IconCall class="footer__banner-icon" />
					<span>+1 800 222 000</span>
				</a>
			</div>
			<div class="footer__content">
				<div class="footer__box">
					<Logo class="footer__logo" />
					<p class="footer__text">
						We are providing high-quality courses for about ten years.
					</p>
					<ul class="footer__links">
						<li class="footer__links-item">
							<a href="#">Fb.</a>
						</li>
						<li class="footer__links-item">
							<a href="#">Ig.</a>
						</li>
						<li class="footer__links-item">
							<a href="#">Tw.</a>
						</li>
						<li class="footer__links-item">
							<a href="#">Be.</a>
						</li>
					</ul>
				</div>
				<div class="footer__box">
					<h2 class="footer__title">Need help?</h2>
					<div>
						<p class="footer__text">Call us directly?</p>
						<a href="tel:+1 800 222 000" class="footer__a footer__a--tel"
							>+1 800 222 000</a
						>
					</div>
					<div>
						<p class="footer__text">Need support?</p>
						<a class="footer__a" href="mailto:help@domain.com">help@domain.com</a>
					</div>
				</div>
				<div class="footer__box">
					<h2 class="footer__title">Subscribe to our newsletter</h2>
					<form class="footer__form" @submit.prevent="submitMail">
						<input
							required
							v-model="mail"
							type="email"
							name="mail"
							class="footer__input"
							placeholder="Enter your email ..." />
						<button class="footer__button">
							<span>Submit</span>
							<span>&rightarrow;</span>
						</button>
						<p :class="{ sent: isMailSent }" class="footer__sent">
							Thank you for subscribing!
						</p>
					</form>
					<div>
						<IconHandshake class="footer__handshake" />
						<p>Protecting your privacy</p>
					</div>
				</div>
			</div>
			<div class="footer__divider"></div>
			<div class="footer__copyright">
				<p>
					&copy; {{ new Date().getFullYear() }} Mindforge is Proudly Developed by
					<a href="http://spacelabs.uz" target="_blank" rel="noopener noreferrer"
						>SpaceLabs</a
					>
				</p>
			</div>
		</footer>
	</section>
</template>

<script setup>
import { ref } from 'vue';
import Button from './Button.vue';
import IconCall from './icons/IconCall.vue';
import Logo from './icons/Logo.vue';
import IconHandshake from './icons/IconHandshake.vue';

const mail = ref();
const isMailSent = ref(false);
const submitMail = () => {
	console.log(mail.value);
	mail.value = '';
	isMailSent.value = true;
	setTimeout(() => {
		isMailSent.value = false;
	}, 2000);
};
</script>

<style lang="scss" scoped>
.footer {
	background-image: linear-gradient(to right bottom, #313e3b, #2e3b38, #2c3835, #293532, #27322f);
	position: relative;
	display: flex;
	flex-direction: column;
	gap: 5rem;
	color: var(--medium-gray);
	padding-bottom: 3rem;
	padding-top: 15rem;

	@media screen and (max-width: 550px) {
		padding-top: 5rem;
	}
	&__form + div {
		display: flex;
		align-items: center;
		gap: 1rem;
	}
	&__sent {
		position: absolute;
		bottom: -6rem;
		left: 0;
		background: #fff;
		padding: 1.5rem 2rem;
		width: 100%;
		border-radius: 4px;
		color: #5cb85c;
		transform: translateY(-15px);
		opacity: 0;
		transition: transform 0.5s, opacity 0.5s;
		&.sent {
			transform: translateY(0);
			opacity: 1;
		}
	}
	&__form {
		background-color: var(--dark-gray);
		padding: 1.5rem 2rem;
		display: flex;
		gap: 3rem;
		position: relative;
		border: 1px solid var(--medium-gray);
		border-radius: 4px;
		transition: border-color 300ms;
		margin: 1rem 0;
		max-width: 80%;
		&:has(input:user-invalid) {
			border-color: #dc3545;
		}
	}
	&__input {
		background-color: transparent;
		border: none;
		color: #fff;
		font: inherit;
		font-size: 15px;
		outline: none;
		width: 100%;
	}
	&__button {
		background-color: transparent;
		border: none;
		color: #fff;
		font-size: 15px;
		cursor: pointer;
		transition: color 300ms;
		display: flex;
		gap: 10px;

		& > span:last-of-type {
			transition: transform 300ms;
		}

		&:hover {
			color: var(--base-color);
			& > span:last-of-type {
				transform: translateX(5px);
			}
		}
	}
	&__copyright {
		display: flex;
		justify-content: center;
		line-height: 2;
		text-align: center;
		transform: translateY(2rem);
		opacity: 0;
		transition: transform 300ms, opacity 300ms;
		transition-delay: 1.5s;
		a {
			color: #fff;
			font-weight: 500;
		}
	}
	&__a {
		color: #fff;
		font-size: 17px;
		transition: color 300ms;
		&:hover {
			color: var(--base-color);
		}
		&--tel {
			text-decoration: none;
		}
	}
	&__links {
		list-style: none;
		font-size: 18px;
		font-weight: 500;
		display: flex;
		gap: 15px;
		margin-top: 15px;
		&-item {
			a {
				color: #fff;
				text-decoration: none;
				transition: color 300ms;
				&:hover {
					color: var(--base-color);
				}
			}
		}
	}
	& > * {
		z-index: 1;
	}
	&__banner {
		position: absolute;
		left: 50%;
		top: 0;
		transform: translate(-50%, -50%);
		z-index: 10;
		width: 80%;
		background-color: var(--base-color);
		display: flex;
		align-items: center;
		gap: 3rem;
		padding: 3.6rem min(6vw, 6rem);
		border-radius: 8px;
		background-image: url('@/assets/images/cta-bg.webp');
		background-repeat: no-repeat;
		flex-wrap: wrap;
		@media screen and (max-width: 550px) {
			position: static;
			transform: none;
			width: 100%;
			text-align: center;
		}
		&-title {
			font-size: 28px;
			font-weight: 600;
			font-family: var(--font-alt);
			color: var(--dark-gray);
		}
		a {
			text-decoration: none;
		}
		&-button {
			background-color: var(--dark-gray);
			color: #fff;
		}
		&-call {
			color: var(--dark-gray);
			font-size: 19px;
			font-weight: 600;
			display: flex;
			align-items: center;
			gap: 1rem;
		}
		&-icon {
			width: 1.7rem;
			height: 1.7rem;
		}
	}
	&__box {
		display: flex;
		flex-direction: column;
		gap: 15px;
		opacity: 0;
		transform: translateX(-100%);
		transition: opacity 800ms, transform 800ms;
		&:nth-of-type(2) {
			transition-delay: 300ms;
		}
		&:nth-of-type(3) {
			transition-delay: 600ms;
		}
		@media only screen and (max-width: 550px) {
			align-items: center;
			text-align: center;
		}
		&:first-of-type p {
			max-width: 25ch;
		}
	}
	&__title {
		font-size: 18px;
		color: #fff;
		font-weight: 500;
	}
	&__text {
		line-height: 28px;
		font-size: 17px;
	}
	&__content {
		display: flex;
		flex-wrap: wrap;
		column-gap: 10rem;
		row-gap: 7rem;
		@media only screen and (max-width: 550px) {
			justify-content: center;
		}
	}
	&__divider {
		width: 100%;
		height: 1px;
		background-color: rgba(255, 255, 255, 0.1);
	}
	&__logo {
		width: 15.7rem;
		height: 4rem;
	}
	&__obj {
		position: absolute;
		left: -10rem;
		top: 2rem;
		width: 32rem;
	}
	&__lines {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-image: url('@/assets/images/hero-lines.svg');
		background-size: 12.5rem;
	}
}

.section.active .footer__box {
	opacity: 1;
	transform: translateX(0);
}
.section.active .footer__copyright {
	opacity: 1;
	transform: translateY(0);
}
</style>
