<script>
	import { onMount } from 'svelte';

	let theme = $state('dark');
	
	const cards = [
		{
			title: 'Return Home',
			location: 'Voyage in Pescara',
			image: 'https://www.figma.com/api/mcp/asset/438956fc-1ce2-4942-b5cd-07f9ea073b80'
		},
		{
			title: 'When Sky touched Sea',
			location: 'Adriatic Sea, Pescara',
			image: 'https://www.figma.com/api/mcp/asset/59bd0f87-fc5a-468f-951d-8d03b4990712'
		},
		{
			title: 'Chinese New Year',
			location: 'Milan',
			image: 'https://www.figma.com/api/mcp/asset/6312f923-bb04-4fb7-ac34-8a1c2be4c69b'
		},
		{
			title: 'Elektra',
			location: 'Gae Aulenti exhibition',
			image: 'https://www.figma.com/api/mcp/asset/66f64bc7-69bf-4b34-8096-e994eed2cc0d'
		},
		{
			title: 'Japanese Secret Garden',
			location: 'Malta',
			image: 'https://www.figma.com/api/mcp/asset/7f7e00b0-2bb3-4522-8b74-e5bdc1019b8e'
		},
		{
			title: 'Am I a writer?',
			location: 'Me',
			image: 'https://www.figma.com/api/mcp/asset/d1065f03-d7c3-4818-8ec1-c73ef37b2692'
		},
		{
			title: 'The oxymoron dark-light',
			location: 'Gae Aulenti exhibition',
			image: 'https://www.figma.com/api/mcp/asset/a78c2eec-d9ec-46fd-8a6b-dba504bad36a'
		},
		{
			title: 'Japanese Secret Garden',
			location: 'Malta',
			image: 'https://www.figma.com/api/mcp/asset/2eb1d6e2-b9da-45c3-a97b-a26d4348296f'
		},
		{
			title: 'The Artist among Artists',
			location: 'Van Gogh Museum, Trieste',
			image: 'https://www.figma.com/api/mcp/asset/31c308a4-648c-4e8c-a41b-7105a92e9e1a'
		},
		{
			title: 'The Unknown',
			location: 'Milan',
			image: 'https://www.figma.com/api/mcp/asset/b0f874f7-fcb0-440d-a714-fac2dca0ab11'
		}
	];

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
		<a href="/about">About</a>
		<a href="/hobby" aria-current="page">Hobby</a>
		<button class="theme-toggle" type="button" onclick={toggleTheme} aria-label="Toggle dark and light mode">
			{theme === 'dark' ? '☀️' : '🌙'}
		</button>
	</nav>
</header>

<section class="landing-shell">
	<div class="hero-copy">
		<p>
			I move between <span class="highlight">stories</span> and <span class="highlight">systems</span>, writing worlds on paper <br>and building them in code, letting imagination and logic shape<br> each other until ideas become experiences.
		</p>
	</div>

	<main class="landing-content">
		<section class="text-panel">
			<p>
				Writing has been my first creative home. Since I was a child, I’ve dreamed of becoming a writer, filling notebooks with stories, characters, and ideas that I hoped would one day grow into real books. That desire never left; it evolved with me. Today, writing remains a space where I explore imagination, emotion, and narrative structure - a practice that continues to shape how I think, observe, and design.
			</p>
			<p>
				On the other side of my creative identity lies a passion that emerged during my high-school years: computer science and programming. What began as curiosity quickly became a second love - one rooted in logic, experimentation, and the thrill of building something from scratch. Over time, this interest expanded into web design and game design, fields where storytelling and interactivity meet. The technical experience I gained during my scientific studies gave me the tools to transform ideas into functioning digital experiences, turning what once felt like a distant fascination into a concrete reality.
			</p>
		</section>
	</main>

	<footer class="landing-footer">
		<div class="footer-logo-wrap">
			<img
				class="footer-logo"
				src="https://www.figma.com/api/mcp/asset/a8c85964-30a6-4f5d-9842-9283e5052482"
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
		background: radial-gradient(circle at top left, rgba(166, 125, 255, 0.18), transparent 24%),linear-gradient(180deg, var(--color-surface-soft), var(--color-surface));
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