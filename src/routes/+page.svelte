<script lang="ts">
	import { onMount } from 'svelte';
// if you are going to use `loadSlim`, install the "tsparticles-slim" package too.
	import { cubicOut } from 'svelte/easing';
	import { fade } from 'svelte/transition';
	import type { PageData } from './$types';

	export let data: PageData;

	let particlesConfig = {
		particles: {
			color: {
				value: '#FFF'
			},
			links: {
				enable: true,
				color: '#FFF'
			},
			move: {
				enable: true
			},
			number: {
				value: 100
			},
			size: {
				value: 3
			},
			// make blurry
			opacity: {
				value: 0.15,
				random: true,
				anim: {
					enable: true,
					speed: 1
				}
			}
		}
	};

	let particlesInit = async (engine: Engine) => {
		await loadSlim(engine);
	};

	let state: 'home' | 'features' | 'discord' = 'home';
	let routes = ['home', 'features', 'discord'];
</script>

<main>
	<nav>
		<div class="navbar-container">
			<div class="navbar-left">
				<img
					src="https://media.discordapp.net/attachments/1151595849940467756/1155291328700227584/image-removebg-preview_5.png?width=249&height=249"
					alt="logo"
				/>
				<span> shuttle.rip </span>

				<div class="navbar-links">
					{#each routes as route}
						<!-- svelte-ignore a11y-click-events-have-key-events -->
						<!-- svelte-ignore a11y-missing-attribute -->
						<a
							on:click={() => (state = route)}
							style={state === route ? 'scale: 1.05; color: #fff;' : ''}
						>
							{route}
						</a>
					{/each}
				</div>
			</div>
			<div class="navbar-buttons">
				{#if data.session}
					<a href="/dashboard"> Dashboard </a>
				{:else}
				<a href="/register"> Log in </a>
				<a href="/login"> Register </a>
				{/if}
			</div>
		</div>
	</nav>

	{#if state === 'home'}
		<div class="content-container" in:fade={{ duration: 500, delay: 0, easing: cubicOut }}>
			<div class="text-container">
				<h1>shuttle.rip</h1>
				<p>A streamlined biolink experience</p>
			</div>
			<div class="stats-container">
				<div class="stat">
					<h1>69</h1>
					<p>Users</p>
				</div>
				<div class="stat">
					<h1>420</h1>
					<p>Views</p>
				</div>
			</div>
			<a href="/register">Get started 🚀</a>
		</div>
	{:else if state === 'features'}
		<div class="content-container" in:fade={{ duration: 500, delay: 0, easing: cubicOut }}>
			<div class="text-container">
				<h1>Features</h1>
				<p>Customize your biolink with a variety of features</p>
			</div>

			<div class="feature-grid">
				<div class="feature-grid-card">
					<h3>
						Interactive Dashboard 
					</h3>
					<p>
						Our dashboard is easy to use and allows you to customize your biolink with
						ease.
					</p>
				</div>
				<div class="feature-grid-card">
					<h3>Unique Profile Card</h3>
					<p>
						Your profile card is unique to you and allows you to show off your socials.
					</p>
				</div>
				<div class="feature-grid-card">
					<h3>Data Security</h3>
					<p>
						Your data and personal information is safe with us. We don't sell your data
						to third parties.
					</p>
				</div>
				<div class="feature-grid-card">
					<h3>Support</h3>
					<p>
						We have a dedicated support team to help you with any issues you may have.
					</p>
				</div>
			</div>
		</div>
	{:else if state === 'discord'}
		<div class="content-container" in:fade={{ duration: 500, delay: 0, easing: cubicOut }}>
			<div class="text-container">
				<h1>Join our Discord</h1>
				<p>Join our Discord to get support and stay up to date with the latest updates</p>
			</div>
			<a href="https://discord.gg/shuttlebio">Join our Discord</a>
		</div>
	{/if}

	<div class="background">
	</div>
</main>

<style lang="scss">
	main {
		height: 100vh;
		width: 100vw;
		display: flex;
		justify-content: center;
		align-items: center;
		overflow: hidden;

		nav {
			position: fixed;
			top: 12px;
			width: 100%;
			max-width: 650px;
			border-radius: 3rem;
			padding: 12px;
			background-color: rgba(38, 38, 35, 0.5);

			.navbar-container {
				display: flex;
				justify-content: space-between;
				align-items: center;
				width: 100%;
				height: 100%;

				.navbar-left {
					// align the logo and text vertically but side by side
					display: flex;
					flex-direction: row;

					align-items: center;

					img {
						height: 30px;
						width: 30px;
						margin-right: 10px;
					}

					span {
						font-size: 1rem;
						font-weight: 600;
						color: #fff;
					}

					.navbar-links {
						display: flex;
						flex-direction: row;
						align-items: center;
						margin-left: 12px;

						a {
							// shouldnt look like a button just a link
							background-color: transparent;
							border-radius: 0;
							margin-left: 12px;
							color: var(--color-text);
							text-decoration: none;
							font-size: 0.9rem;
							transition: all 0.2s ease-in-out;

							&:hover {
								scale: 1.05;
							}
						}

						@media screen and (max-width: 600px) {
							display: none;
						}
					}
				}

				.navbar-buttons {
					display: flex;
					flex-direction: row;
					align-items: center;

					a {
						text-decoration: none;
						color: var(--color-background);
						margin-left: 12px;
						background-color: var(--color-heading);
						padding: 5px 15px;
						border-radius: 1rem;
						transition: all 0.2s ease-in-out;

						&:hover {
							transform: translateY(2px);
						}
					}
				}
			}
		}

		.content-container {
			backdrop-filter: blur(16px);
			background-color: rgba(68, 64, 60, 0.1);
			border: 1px solid rgb(41, 37, 36);
			border-radius: 12px;
			width: 100%;
			max-width: 650px;
			height: 100%;
			max-height: 500px;
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: space-evenly;
			padding: 12px;
			text-align: center;

			.text-container {
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;
				width: 100%;

				h1 {
					font-size: 2.5rem;
					font-weight: 600;
					color: var(--color-text);
					margin-bottom: 12px;
					margin: 0;
				}

				p {
					font-size: 1.2rem;
					font-weight: 400;
					color: var(--color-text-muted);
					margin: 0;
				}
			}

			.stats-container {
				display: flex;
				flex-direction: row;
				align-items: center;
				justify-content: space-between;
				margin-top: 12px;
				width: 100%;
				max-width: 200px;

				.stat {
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;

					h1 {
						font-size: 1.25rem;
						font-weight: 500;
						color: var(--color-text);
						margin-bottom: 12px;
						margin: 0;
					}

					p {
						font-size: 1rem;
						font-weight: 400;
						color: var(--color-text-muted);
						margin: 0;
					}
				}
			}

			.feature-grid {
				display: grid;
				grid-template-columns: repeat(2, 1fr);
				grid-template-rows: repeat(2, 1fr);
				grid-gap: 12px;
				width: 100%;
				max-width: 650px;
				margin-top: 12px;

				.feature-grid-card {
					display: flex;
					flex-direction: column;
					justify-content: center;
					background-color: rgba(68, 64, 60, 0.1);
					border: 1px solid rgb(41, 37, 36);
					border-radius: 12px;
					padding: 12px;

					h3 {
						font-size: 1.25rem;
						font-weight: 500;
						color: var(--color-text);
						margin-bottom: 12px;
						margin: 0;
					}

					p {
						font-size: 1rem;
						font-weight: 400;
						color: var(--color-text-muted);
						margin: 0;
					}
				}
			}

			a {
				text-decoration: none;
				color: var(--color-background);
				margin-top: 12px;
				background-color: var(--color-heading);
				padding: 10px 20px;
				border-radius: 1rem;
				transition: all 0.2s ease-in-out;

				&:hover {
					scale: 1.05;
				}
			}
		}

		.background {
			position: fixed;
			top: 0;
			left: 0;
			width: 100%;
			height: 100%;
			z-index: -1;
			filter: blur(4px);

			#tsparticles {
				height: 100%;
				width: 100%;
			}
		}
	}
</style>
