<template>
	<section class="section">
		<footer class="footer section-padding">
			<div class="footer__lines"></div>
			<img class="footer__obj" src="@/assets/images/offer-obj.png" />
			<div class="footer__banner">
				<FooterPattern class="footer__banner-back" />
				<h1 class="footer__banner-title">
					“{{ $t('footer-strong') }} {{ $t('footer-power') }}”
				</h1>
			</div>
			<div class="footer__content">
				<div class="footer__box">
					<LogoWhite class="footer__logo" />
					<p class="footer__text">{{ $t('footer-subtitle') }}</p>
					<ul class="footer__links">
						<li class="footer__links-item">
							<a
								target="_blank"
								href="https://www.facebook.com/profile.php?id=61565196746663">
								<IconFacebook />
							</a>
						</li>
						<li class="footer__links-item">
							<a target="_blank" href="https://www.instagram.com/mindforge.uz/">
								<IconInsta />
							</a>
						</li>
						<li class="footer__links-item">
							<a target="_blank" href="https://t.me/mindforge_edu">
								<IconTelegram />
							</a>
						</li>
					</ul>
				</div>
				<div class="footer__box">
					<h2 class="footer__title">{{ $t('footer-help') }}</h2>
					<div>
						<p class="footer__text">{{ $t('footer-call') }}</p>
						<a href="tel:+998 90 950 74 02" class="footer__a footer__a--tel"
							>+998 90 950 74 02</a
						>
					</div>
					<div>
						<p class="footer__text">{{ $t('footer-support') }}</p>
						<a class="footer__a" href="mailto:info@mindforge.uz">info@mindforge.uz</a>
					</div>
				</div>
			</div>
			<div class="footer__divider"></div>
			<div class="footer__copyright">
				<p>
					&copy; {{ new Date().getFullYear() }} Mindforge. {{ $t('dev') }}
					<a href="http://spacelabs.uz" target="_blank" rel="noopener noreferrer"
						>Space Labs</a
					>
				</p>
			</div>
		</footer>
	</section>
</template>

<script setup>
import Circle from './Circle.vue';
import FooterPattern from './FooterPattern.vue';
import IconFacebook from './icons/IconFacebook.vue';
import IconInsta from './icons/IconInsta.vue';
import IconTelegram from './icons/IconTelegram.vue';
import Logo from './icons/Logo.vue';
import LogoWhite from './LogoWhite.vue';
import Rectangle from './Rectangle.vue';
import Triangle from './Triangle.vue';
</script>

<style lang="scss" scoped>
.footer {
	background-image: linear-gradient(to right bottom, #246294, #184e77, #123d5c, #0f2d44, #0b1f30);
	position: relative;
	display: flex;
	flex-direction: column;
	gap: 5rem;
	color: var(--medium-gray);
	padding-bottom: 3rem;
	padding-top: 15rem;
	margin-top: 6rem;

	@media screen and (max-width: 550px) {
		padding-top: 5rem;
	}

	&__copyright {
		display: flex;
		justify-content: center;
		line-height: 2;
		text-align: center;
		transform: translateY(2rem);
		opacity: 0;
		transition: transform 300ms, opacity 300ms;
		transition-delay: 800ms;
		a {
			color: #fff;
			font-weight: 500;
			transition: color 300ms;
			text-decoration: none;
			&:hover {
				color: var(--base-color);
			}
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
				text-decoration: none;
				transition: color 300ms;
				svg {
					fill: #fff;
					transition: fill 300ms;
				}
				&:hover svg {
					fill: var(--base-color);
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
		background-color: #072036;
		display: flex;
		align-items: center;
		gap: 1.5rem;
		padding: 2rem min(6vw, 6rem);
		border-radius: 8px;
		text-align: center;
		justify-content: center;
		color: #fff;
		position: relative;
		overflow: hidden;

		&-back {
			position: absolute;
			width: 100%;
			@media only screen and (max-width: 1200px) {
				height: 100%;
				width: 200%;
			}
		}
		&-svgs {
			position: absolute;
			inset: 0;
			display: flex;
			align-items: center;
			height: 100%;
			width: 100%;
			z-index: -1;
			opacity: 0.3;

			& > * {
				width: 100%;
			}
		}
		@media screen and (max-width: 550px) {
			position: relative;
			left: 0;
			top: 0;
			transform: none;
			width: 100%;
			text-align: center;
		}
		&-title {
			font-size: 3.6rem;
			font-family: var(--font-alt);
			font-weight: 700;
			text-transform: uppercase;
			color: #fff;
			z-index: 2;
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
	&__circle {
		transform: translateX(-25%);
		animation: rotateY 10s infinite alternate;
	}
	&__rectangle {
		transform: rotate(44deg);
		animation: rotate 15s infinite alternate;
	}
	&__triangle {
		transform: rotate(-45deg);
		animation: rotate-reverse 20s infinite alternate;
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
			transition-delay: f;
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
		width: 13.7rem;
		height: 4rem;
		color: #fff;
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
@keyframes rotate {
	0% {
		transform: rotate(0);
	}
	100% {
		transform: rotate(360deg);
	}
}
@keyframes rotate-reverse {
	0% {
		transform: rotate(0);
	}
	100% {
		transform: rotate(-360deg);
	}
}
@keyframes rotateY {
	0% {
		transform: rotateY(0);
	}
	100% {
		transform: rotateY(360deg);
	}
}
</style>
