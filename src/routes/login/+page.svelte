<script lang="ts">
	import { Turnstile } from 'svelte-turnstile';

	export let form: any;
</script>

<main>
	{#if form?.error}<p>{form.error}</p>{/if}
	<h1>login</h1>
	<p>don't have an account? <b><a href="/register">register</a></b></p>
	<form action="?/login" method="POST" class="auth-form">
		<input type="text" name="email" placeholder="email" />
		<input type="password" name="password" placeholder="password" />
		<Turnstile siteKey="0x4AAAAAAAKMyxv1BmHMiYDO" theme="dark" />
		<button type="submit" class="btn btn-primary">login</button>
		<p>forgot your password? <b><a href="/recover">recover</a></b></p>
	</form>
</main>

<style lang="scss">
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: 100vh;
		text-align: center;

		h1 {
			font-size: 3rem;
			margin-bottom: 0;
		}

		b {
			font-weight: bold;
		}

		a {
			text-decoration: none;
			color: inherit;

			&:hover {
				text-decoration: underline;
			}
		}

		form {
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			text-align: center;
			margin-top: 2rem;

			input {
				background-color: transparent;
				border: none;
				border-bottom: 1px solid var(--color-text);
				color: var(--color-text);
				font-family: var(--font-family);
				font-size: 1rem;
				margin: 1rem;
				padding: 0.5rem;
				width: 20rem;
				transition: all 0.2s ease-in-out;

				// make background white when focused
				&:focus {
					outline: none;
					background-color: var(--color-background-soft);
					filter: invert(1) brightness(0.85);
				}
			}

			button {
				padding: 7px 70px;
				width: 100%;
				font-family: var(--font-family);
				font-size: 14px;
				font-weight: 700;
				margin-top: 30px;
				border: none;
				border-radius: 36px;
				cursor: pointer;
				transition: 0.2s ease-in-out;
				background-color: var(--color-background-soft);
				color: var(--color-text);
				transition: all 0.3s ease-in-out;

				&:hover {
					filter: invert(1) brightness(0.85);
					transform: scale(1.05);
				}

				&:active {
					transform: scale(0.95);
				}

				&:focus {
					outline: none;
				}
			}
		}
	}

	@media (max-width: 600px) {
		main {
			h1 {
				font-size: 2rem;
			}

			p {
				font-size: 1.25rem;
			}
		}
	}
</style>
