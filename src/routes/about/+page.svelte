<script>
	import { onMount } from 'svelte';
	import politecnicoLogo from '$lib/assets/images_cards/Politecnico_Bianco 1.png';

	let theme = $state('dark');

	/** @param {'light' | 'dark'} value */
	const applyTheme = (value) => {
		theme = value;
		document.documentElement.dataset.theme = value;
		localStorage.setItem('theme', value);
	};

	const toggleTheme = () => applyTheme(theme === 'dark' ? 'light' : 'dark');

	onMount(() => {
		const storedTheme = localStorage.getItem('theme');
		const systemPreferred = window.matchMedia('(prefers-color-scheme: light)').matches ? 'light' : 'dark';
		const nextTheme = storedTheme === 'light' || storedTheme === 'dark' ? storedTheme : systemPreferred;
		applyTheme(nextTheme);
	});
</script>

<header class="topbar">
	<a class="brand" href="/"><span>Ss</span><span class="dot">.</span></a>
	<nav class="nav-links" aria-label="Primary navigation">
		<a href="/about" aria-current="page">About</a>
		<a href="/hobby">Hobby</a>
		<button class="theme-toggle" type="button" onclick={toggleTheme} aria-label="Toggle dark and light mode">
			{theme === 'dark' ? '☀️' : '🌙'}
		</button>
	</nav>
</header>

<section class="landing-shell">
	<div class="hero-copy">
		<p>
			I am Serah, and this space is where I collect study projects,<br>
			visual notes, and ideas that become small stories.<br>
			The goal is simple: to keep creating with care, curiosity,<br>
			and a <span class="highlight">quiet attention to detail</span>.
		</p>
	</div>

	<main class="landing-content">
		<section class="text-panel">
			<p>
				My name is Serena Serafini, and I am a Communication Design student at Politecnico di Milano.
				My academic path began in Abruzzo, where I graduated from the Liceo Scientifico Scienze Applicate Corradino d’Ascanio in Montesilvano, Pescara.
			</p>
			<p>
				I’m passionate about how visual languages shape understanding, and I approach design as a bridge between clarity, creativity, and meaningful communication. My work often explores the intersection between research, visual storytelling, and user‑centered thinking, with a strong interest in how design can make complex ideas accessible.
			</p>
		</section>
	</main>

	<footer class="landing-footer">
		<div class="footer-logo-wrap">
			<img
				class="footer-logo"
				src={politecnicoLogo}
				alt="Politecnico Milano 1863"
				loading="lazy"
			/>
		</div>
		<div class="footer-contact">
			<div class="footer-title">Get in touch</div>
			<a class="footer-link" href="https://www.instagram.com/days_of_serah" target="_blank" rel="noreferrer noopener">@days_of_serah</a>
			<a class="footer-link" href="mailto:serena.serafini@mail.polimi.it">serena.serafini@mail.polimi.it</a>
		</div>
	</footer>
</section>

<style>
	.landing-shell {
		min-height: 100vh;
		padding: 0;
		background: radial-gradient(circle at top left, rgba(166, 125, 255, 0.18), transparent 24%),
			linear-gradient(180deg, var(--color-surface-soft), var(--color-surface));
	}

	.topbar {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 1.4rem 3rem;
		background: linear-gradient(90deg, rgba(166, 125, 255, 0.9) 4.8%, rgba(10, 10, 10, 0.95) 37%);
	}

	.brand {
		display: inline-flex;
		align-items: baseline;
		font-family: var(--font-heading);
		font-size: clamp(1.8rem, 2.3vw, 2.4rem);
		font-weight: 100;
		letter-spacing: 0;
		color: var(--color-white-soft);
		margin-left: -1rem;
		text-decoration: none;
	}

	.brand:visited,
	.brand:hover,
	.brand:focus-visible {
		color: var(--color-white-soft);
		text-decoration: none;
	}

	.brand .dot {
		color: var(--color-purple);
	}

	.nav-links {
		display: flex;
		align-items: center;
		gap: 2rem;
		margin-right: 0.5rem;
	}

	.nav-links a {
		position: relative;
		font-family: var(--font-heading);
		font-size: 0.95rem;
		font-weight: 600;
		font-variation-settings: "wdth" 100;
		letter-spacing: 0.26em;
		color: var(--color-muted);
		padding-bottom: 0.25rem;
		text-decoration: none;
		transition: color 180ms ease;
	}

	.nav-links a::after,
	.nav-links a::before {
		content: '';
		position: absolute;
		bottom: 0;
		width: 50%;
		height: 2px;
		background: color-mix(in srgb, var(--color-purple-soft) 88%, transparent);
		transform: scaleX(0);
		opacity: 0;
		transition: transform 220ms ease, opacity 220ms ease;
	}

	.nav-links a::after {
		left: 0;
		transform-origin: left center;
	}

	.nav-links a::before {
		right: 0;
		transform-origin: right center;
	}

	.nav-links a:hover,
	.nav-links a:focus-visible,
	.nav-links a[aria-current='page'] {
		color: var(--color-purple-soft);
		text-shadow: 0 0 14px color-mix(in srgb, var(--color-purple-soft) 28%, transparent);
	}

	.nav-links a:hover::after,
	.nav-links a:hover::before,
	.nav-links a:focus-visible::before,
	.nav-links a:focus-visible::after,
	.nav-links a[aria-current='page']::before,
	.nav-links a[aria-current='page']::after {
		transform: scaleX(1);
		opacity: 1;
	}

	.theme-toggle {
		position: relative;
		display: inline-flex;
		align-items: center;
		justify-content: center;
		isolation: isolate;
		border: 1px solid var(--color-border);
		border-radius: 999px;
		padding: 0.85rem 1.1rem;
		font-size: 0.9rem;
		background: color-mix(in srgb, var(--color-surface-soft) 36%, transparent);
		color: var(--color-muted);
		cursor: pointer;
	}

	.theme-toggle:hover {
		border-color: color-mix(in srgb, var(--color-purple) 45%, var(--color-border));
		color: var(--color-text);
		background: color-mix(in srgb, var(--color-surface-soft) 52%, transparent);
	}

	.landing-content {
		max-width: 1512px;
		margin: 0 auto;
		padding: 1.5rem clamp(1.25rem, 5vw, 5rem) 3rem;
	}

	.hero-copy {
		padding: 160px 80px 90px;
	}

	.hero-copy p {
		font-family: var(--font-primary);
		font-weight: 200;
		font-size: 40px;
		line-height: 1.2;
		color: var(--color-white-soft);
		margin: 0;
	}

	.hero-copy .highlight {
		color: #895fad;
	}

	.text-panel {
		max-width: 860px;
		padding: 2rem 0 4rem;
	}

	.text-panel p {
		font-family: var(--font-primary);
		font-size: clamp(1.05rem, 1.4vw, 1.25rem);
		line-height: 1.55;
		color: var(--color-text);
		opacity: 0.9;
		margin: 0 0 1rem;
	}

	.landing-footer {
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: 1rem;
		margin-top: 3rem;
		margin-bottom: 1.5rem;
		padding: 1rem clamp(1.25rem, 5vw, 5rem);
		background: rgba(2, 3, 7, 0.96);
		color: var(--color-text);
	}

	.footer-logo-wrap {
		width: 201px;
		height: 78px;
		flex: 0 0 auto;
	}

	.footer-logo {
		width: 100%;
		height: 100%;
		object-fit: contain;
		display: block;
	}

	.footer-title {
		font-family: var(--font-heading);
		font-size: clamp(1.2rem, 1.6vw, 1.5rem);
		font-weight: 700;
		line-height: 0.92;
		color: var(--color-text);
	}

	.footer-contact {
		display: flex;
		flex-direction: column;
		align-items: flex-end;
		gap: 0.3rem;
		text-align: right;
	}

	.footer-link {
		font-family: var(--font-primary);
		font-size: clamp(1rem, 1.25vw, 1.25rem);
		font-weight: 300;
		line-height: 1.15;
		color: var(--color-text);
		text-decoration: none;
		opacity: 0.92;
	}

	.footer-link:hover {
		color: var(--color-purple-soft);
		opacity: 1;
	}

	:global(html[data-theme='light']) .topbar {
		background: linear-gradient(90deg, rgba(166, 125, 255, 0.9) 4.8%, rgba(255, 255, 255, 0.95) 37%);
	}

	:global(html[data-theme='light']) .brand,
	:global(html[data-theme='light']) .brand:hover,
	:global(html[data-theme='light']) .brand:visited,
	:global(html[data-theme='light']) .brand:focus-visible {
		color: #121212;
	}

	:global(html[data-theme='light']) .landing-shell {
		background: var(--color-surface);
	}

	:global(html[data-theme='light']) .nav-links a {
		color: #151515;
	}

	:global(html[data-theme='light']) .nav-links a:hover,
	:global(html[data-theme='light']) .nav-links a:focus-visible,
	:global(html[data-theme='light']) .nav-links a[aria-current='page'] {
		color: var(--color-purple-soft);
	}

	:global(html[data-theme='light']) .theme-toggle {
		background: color-mix(in srgb, #ffffff 74%, transparent);
		color: #1d1d1d;
		border-color: rgba(20, 20, 20, 0.24);
	}

	:global(html[data-theme='light']) .hero-copy p {
		color: #181126;
	}

	:global(html[data-theme='light']) .landing-footer {
		background: var(--color-surface-soft);
		color: #1d1d1d;
	}

	:global(html[data-theme='light']) .footer-logo {
		mix-blend-mode: exclusion;
	}

	:global(html[data-theme='light']) .footer-title {
		color: #1d1d1d;
	}

	:global(html[data-theme='light']) .footer-link {
		color: #1d1d1d;
		opacity: 1;
	}

	:global(html[data-theme='light']) .footer-link:hover {
		color: var(--color-purple-soft);
		text-shadow: 0 0 14px color-mix(in srgb, var(--color-purple-soft) 28%, transparent);
		opacity: 1;
	}

	@media (max-width: 680px) {
		.topbar {
			flex-direction: column;
			align-items: flex-start;
		}

		.nav-links {
			gap: 1rem;
		}

		.hero-copy {
			padding: 80px 24px 50px;
		}

		.hero-copy p {
			font-size: 1.8rem;
		}

		.landing-footer {
			flex-direction: column;
			align-items: flex-start;
		}

		.footer-contact {
			align-items: flex-start;
			text-align: left;
		}
	}
</style>