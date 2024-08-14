<template>
	<section class="section">
		<footer class="footer section-padding">
			<div class="footer__lines"></div>
			<img class="footer__obj" src="@/assets/images/offer-obj.png" />
			<div class="footer__banner">
				<IconLike />
				<h1 class="footer__banner-title">
					Оставайтесь на связи. Подпишитесь на нас в <a href="#">Facebook</a>
				</h1>
			</div>
			<div class="footer__content">
				<div class="footer__box">
					<Logo class="footer__logo" />
					<p class="footer__text">Предоставляем качественный контент уже 6 лет</p>
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
					<h2 class="footer__title">Нужна помощь?</h2>
					<div>
						<p class="footer__text">Позвонить нам?</p>
						<a href="tel:+1 800 222 000" class="footer__a footer__a--tel"
							>+1 800 222 000</a
						>
					</div>
					<div>
						<p class="footer__text">Нужна поддержка?</p>
						<a class="footer__a" href="mailto:help@domain.com">help@domain.com</a>
					</div>
				</div>
			</div>
			<div class="footer__divider"></div>
			<div class="footer__copyright">
				<p>
					&copy; {{ new Date().getFullYear() }} Mindforge. Разработано
					<a href="http://spacelabs.uz" target="_blank" rel="noopener noreferrer"
						>SpaceLabs</a
					>
				</p>
			</div>
		</footer>
	</section>
</template>

<script setup>
import IconLike from './icons/IconLike.vue';
import Logo from './icons/Logo.vue';
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
		gap: 1.5rem;
		padding: 3.6rem min(6vw, 6rem);
		border-radius: 8px;
		background-image: url('@/assets/images/cta-bg.webp');
		background-repeat: no-repeat;
		flex-wrap: wrap;
		text-align: center;
		justify-content: center;
		color: var(--dark-gray);

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
		}
		a {
			color: inherit;
			font-weight: 800;
			transition: color 300ms;
			&:hover {
				color: #fff;
			}
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
		width: 15.7rem;
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
</style>
