<script>
	import { onMount } from 'svelte';

	const years = ["2026", "2025", "2024"];
	let selectedYear = $state("2026");
	let theme = $state('dark');

	const gallery = [
		{
			src: "https://www.figma.com/api/mcp/asset/95575011-9291-473f-b961-7ea18d834b3f",
			title: "Return Home",
			subtitle: "Voyage in Pescara",
			year: "2026"
		},
		{
			src: "https://www.figma.com/api/mcp/asset/d277e29e-4b7b-4f4b-a7e8-7f7bfc463b89",
			title: "When Sky touched Sea",
			subtitle: "Adriatic Sea, Pescara",
			year: "2026"
		},
		{
			src: "https://www.figma.com/api/mcp/asset/7e768e57-4fe0-404f-bc31-24dd65ebeb59",
			title: "Chinese New Year",
			subtitle: "Milan",
			year: "2026"
		},
		{
			src: "https://www.figma.com/api/mcp/asset/a47581b7-950c-402d-a324-ee5200c71a27",
			title: "Elektra",
			subtitle: "Gae Aulenti exhibition",
			year: "2026"
		},
		{
			src: "https://www.figma.com/api/mcp/asset/5b5c0e12-69fe-4778-8169-219afdaefcc7",
			title: "Japanese Secret Garden",
			subtitle: "Malta",
			year: "2025"
		},
		{
			src: "https://www.figma.com/api/mcp/asset/c8dbde01-b611-4a7b-9c2e-1bf0e84ca7c0",
			title: "Am I a writer?",
			subtitle: "Me",
			year: "2025"
		},
		{
			src: "https://www.figma.com/api/mcp/asset/8264ebe0-a272-421b-816f-b6c841c073a6",
			title: "The Unknown",
			subtitle: "Milan",
			year: "2024"
		},
		{
			src: "https://www.figma.com/api/mcp/asset/19486852-7908-4cc5-a7c1-7d784adbdfda",
			title: "The oxymoron dark-light",
			subtitle: "Gae Aulenti exhibition",
			year: "2024"
		},
		{
			src: "https://www.figma.com/api/mcp/asset/c7b6d275-2767-4b20-b01c-51f34bb517c6",
			title: "Japanese Secret Garden",
			subtitle: "Malta",
			year: "2024"
		},
		{
			src: "https://www.figma.com/api/mcp/asset/3902ed26-a2fd-4dca-8f4d-64d454d7b897",
			title: "The Artist among Artists",
			subtitle: "Van Gogh Museum, Trieste",
			year: "2024"
		}
	];

	const displayedGallery = () => gallery.filter((item) => item.year === selectedYear);

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
	<div class="brand"><span>Ss</span><span class="dot">.</span></div>
	<nav class="nav-links" aria-label="Primary navigation">
		<a href="#about">About</a>
		<a href="#hobby">Hobby</a>
		<button class="theme-toggle" type="button" on:click={toggleTheme} aria-label="Toggle dark and light mode">
			{theme === 'dark' ? '☀️' : '🌙'}
		</button>
	</nav>
</header>

<section class="landing-shell">
	<div class="hero-copy">
		<p>
			This landing page collects photographs created<br>
			in a didactic context and transformed into small<br>
			visual stories. They are exercises, yes, but also<br>
			attempts to <span class="highlight">understand the world</span> through light,<br>
			silence, and the space between things.
		</p>
	</div>

	<main class="landing-content">
		<div class="year-controls" role="tablist" aria-label="Select year">
			{#each years as year}
				<button
					class:selected={selectedYear === year}
					type="button"
					aria-pressed={selectedYear === year}
					on:click={() => (selectedYear = year)}
				>
					{year}
				</button>
			{/each}
		</div>

		<div class="gallery-grid">
			{#each displayedGallery() as item}
				<article class="gallery-card">
					<div class="card-image-wrap">
						<img src={item.src} alt={item.title} loading="lazy" />
					</div>
					<div class="card-meta">
						<div class="card-text">
							<span class="card-title">{item.title}</span>
							<span class="card-divider">/</span>
							<span class="card-subtitle">{item.subtitle}</span>
						</div>
						<span class="card-arrow" aria-hidden="true">↗</span>
					</div>
				</article>
			{/each}
		</div>
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
		background: radial-gradient(circle at top left, rgba(166, 125, 255, 0.18), transparent 24%),
			linear-gradient(180deg, var(--color-surface-soft), var(--color-surface));
	}

	.topbar {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 1.4rem 5rem;
		background: linear-gradient(90deg, rgba(166, 125, 255, 0.9) 4.8%, rgba(10, 10, 10, 0.95) 37%);
		border-radius: 0;
		box-shadow: none;
	}

	.brand {
		font-family: var(--font-heading);
		font-size: clamp(1.8rem, 2.3vw, 2.4rem);
		font-weight: 100;
		letter-spacing: 0;
		color: var(--color-white-soft);
		margin-left: -1rem;
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
		font-weight: 900;
		font-variation-settings: "wdth" 100;
		text-transform: none;
		letter-spacing: 0.26em;
		color: var(--color-muted);
		padding-bottom: 0.25rem;
		transition: color 180ms ease;
	}

	.nav-links a::after {
		content: '';
		position: absolute;
		left: 0;
		width: 50%;
		bottom: 0;
		height: 2px;
		background: color-mix(in srgb, var(--color-purple-soft) 88%, transparent);
		transform: scaleX(0);
		transform-origin: left center;
		opacity: 0;
		transition: transform 220ms ease, opacity 220ms ease;
	}

	.nav-links a::before {
		content: '';
		position: absolute;
		right: 0;
		width: 50%;
		bottom: 0;
		height: 2px;
		background: color-mix(in srgb, var(--color-purple-soft) 88%, transparent);
		transform: scaleX(0);
		transform-origin: right center;
		opacity: 0;
		transition: transform 220ms ease, opacity 220ms ease;
	}

	.nav-links a:hover {
		color: var(--color-purple-soft);
		text-shadow: 0 0 14px color-mix(in srgb, var(--color-purple-soft) 28%, transparent);
	}

	.nav-links a:hover::after,
	.nav-links a:hover::before,
	.nav-links a:focus-visible::before,
	.nav-links a:focus-visible::after {
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
		font-weight: 600;
		background: color-mix(in srgb, var(--color-surface-soft) 36%, transparent);
		color: var(--color-muted);
		cursor: pointer;
		box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.12), 0 8px 22px rgba(0, 0, 0, 0.28);
		transition: background 180ms ease, color 180ms ease, transform 180ms ease, box-shadow 220ms ease,
			border-color 180ms ease;
	}

	.theme-toggle::before {
		content: '';
		position: absolute;
		inset: -8px;
		z-index: -1;
		border-radius: inherit;
		background: radial-gradient(circle at 50% 50%, color-mix(in srgb, var(--color-purple) 38%, transparent) 0%, transparent 72%);
		opacity: 0.58;
		filter: blur(7px);
		transform: scale(0.96);
		transition: opacity 220ms ease, transform 220ms ease, filter 220ms ease;
	}

	.theme-toggle:hover {
		border-color: color-mix(in srgb, var(--color-purple) 45%, var(--color-border));
		color: var(--color-text);
		background: color-mix(in srgb, var(--color-surface-soft) 52%, transparent);
		box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 10px 26px rgba(0, 0, 0, 0.32);
	}

	.theme-toggle:hover::before {
		opacity: 0.72;
		filter: blur(8px);
		transform: scale(1.02);
	}

	:global(html[data-theme='light']) .topbar {
		background: linear-gradient(90deg, rgba(166, 125, 255, 0.9) 4.8%, rgba(255, 255, 255, 0.95) 37%);
	}

	:global(html[data-theme='light']) .landing-shell {
		background: var(--color-surface);
	}

	:global(html[data-theme='light']) .brand {
		color: #121212;
	}

	:global(html[data-theme='light']) .brand .dot {
		color: var(--color-purple-soft);
	}

	:global(html[data-theme='light']) .nav-links a {
		color: #151515;
	}

	:global(html[data-theme='light']) .nav-links a::after {
		background: color-mix(in srgb, var(--color-purple-soft) 88%, transparent);
	}

	:global(html[data-theme='light']) .nav-links a::before {
		background: color-mix(in srgb, var(--color-purple-soft) 88%, transparent);
	}

	:global(html[data-theme='light']) .nav-links a:hover,
	:global(html[data-theme='light']) .nav-links a:focus-visible {
		color: var(--color-purple-soft);
		text-shadow: 0 0 14px color-mix(in srgb, var(--color-purple-soft) 28%, transparent);
	}

	.theme-toggle:focus-visible {
		outline: none;
		border-color: color-mix(in srgb, var(--color-purple) 65%, var(--color-border));
		box-shadow: 0 0 0 3px color-mix(in srgb, var(--color-purple) 28%, transparent),
			inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 10px 26px rgba(0, 0, 0, 0.32);
	}

	:global(html[data-theme='light']) .theme-toggle {
		background: color-mix(in srgb, #ffffff 74%, transparent);
		color: #1d1d1d;
		border-color: rgba(20, 20, 20, 0.24);
		box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.86), 0 8px 18px rgba(53, 37, 121, 0.14);
	}

	:global(html[data-theme='light']) .theme-toggle::before {
		background: radial-gradient(circle at 50% 50%, color-mix(in srgb, var(--color-purple) 26%, transparent) 0%, transparent 72%);
		opacity: 0.46;
		filter: blur(8px);
	}

	:global(html[data-theme='light']) .theme-toggle:hover {
		box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.96), 0 10px 22px rgba(53, 37, 121, 0.18);
	}

	.brand .dot {
		color: var(--color-purple);
	}

	.landing-content {
		max-width: 1512px;
		margin: 0 auto;
		padding: 1.5rem clamp(1.25rem, 5vw, 5rem) 3rem;
	}

	.hero-copy {
		padding: 160px 80px;
		margin-bottom: 2rem;
	}

	.hero-copy p {
		font-family: var(--font-primary);
		font-weight: 200;
		font-size: 40px;
		line-height: 1.2;
		color: var(--color-white-soft);
		letter-spacing: 0.01em;
		margin: 0;
		text-align: left;
	}

	.hero-copy .highlight {
		color: #895fad;
	}

	:global(html[data-theme='light']) .hero-copy p {
		color: #181126;
	}

	.year-controls {
		display: inline-flex;
		align-items: center;
		gap: 1.5rem;
		margin-bottom: 2.5rem;
		padding-inline: 0.1rem;
	}

	.year-controls button {
		border: none;
		border-radius: 999px;
		padding: 0.5rem 1rem;
		font-family: var(--font-heading);
		font-size: clamp(1.25rem, 1.8vw, 1.5rem);
		font-weight: 700;
		line-height: 0.92;
		letter-spacing: 0;
		background: transparent;
		color: var(--color-text);
		cursor: pointer;
		transition: color 180ms ease, background 180ms ease, transform 180ms ease, box-shadow 180ms ease;
	}

	.year-controls button:hover {
		color: color-mix(in srgb, var(--color-text) 80%, var(--color-purple));
		transform: translateY(-1px);
	}

	.year-controls button.selected {
		background: #895fad;
		color: #f5f5f5;
		border-radius: 999px;
		box-shadow: 0 8px 22px rgba(137, 95, 173, 0.34);
	}

	:global(html[data-theme='light']) .year-controls button {
		color: #2f2547;
	}

	:global(html[data-theme='light']) .year-controls button.selected {
		background: #895fad;
		color: #f8f5ff;
		border-radius: 999px;
		box-shadow: 0 8px 20px rgba(98, 64, 135, 0.2);
	}

	.gallery-grid {
		display: grid;
		grid-template-columns: repeat(2, minmax(0, 1fr));
		column-gap: 1.5rem;
		row-gap: 0;
		align-items: start;
	}

	.gallery-card {
		display: flex;
		flex-direction: column;
		gap: 0;
		padding-bottom: 1.5rem;
		background: transparent;
		border: none;
		border-radius: 0;
		box-shadow: none;
	}

	.card-image-wrap {
		position: relative;
		isolation: isolate;
		aspect-ratio: 664 / 400;
		overflow: hidden;
	}

	.card-image-wrap::after {
		content: '';
		position: absolute;
		inset: 0;
		background: linear-gradient(130deg, rgba(137, 95, 173, 0.4) 0%, rgba(166, 125, 255, 0.26) 42%, rgba(48, 25, 78, 0.34) 100%);
		opacity: 0;
		pointer-events: none;
		transition: opacity 240ms ease;
	}

	.gallery-card img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		display: block;
		transition: transform 260ms ease, filter 260ms ease;
	}

	.card-image-wrap:hover img {
		transform: scale(1.02);
		filter: saturate(1.08) contrast(1.03);
	}

	.card-image-wrap:hover::after {
		opacity: 1;
	}

	.card-meta {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 1rem;
		padding: 0.9rem 0 1rem;
	}

	.card-text {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		min-width: 0;
		font-family: var(--font-primary);
		font-size: clamp(1.1rem, 1.7vw, 1.5rem);
		font-weight: 300;
		line-height: 1.12;
		white-space: nowrap;
	}

	.card-title {
		color: var(--color-text);
	}

	.card-divider,
	.card-subtitle {
		color: var(--color-muted);
	}

	.card-divider {
		flex: 0 0 auto;
	}

	.card-subtitle {
		overflow: hidden;
		text-overflow: ellipsis;
	}

	.card-arrow {
		flex: 0 0 auto;
		display: grid;
		place-items: center;
		width: 2rem;
		height: 2rem;
		font-size: 1.35rem;
		line-height: 1;
		color: var(--color-muted);
		opacity: 0;
		transform: translateY(4px);
		transition: opacity 220ms ease, transform 220ms ease, color 220ms ease;
	}

	.card-image-wrap:hover + .card-meta .card-arrow {
		opacity: 1;
		transform: translateY(0);
		color: var(--color-text);
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

	.footer-contact {
		display: flex;
		flex-direction: column;
		align-items: flex-end;
		gap: 0.3rem;
		text-align: right;
	}

	.footer-title {
		font-family: var(--font-heading);
		font-size: clamp(1.2rem, 1.6vw, 1.5rem);
		font-weight: 700;
		line-height: 0.92;
		color: var(--color-text);
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
		color: #1d1d1d;
		opacity: 1;
	}

	@media (max-width: 900px) {
		.gallery-grid {
			grid-template-columns: 1fr;
			row-gap: 1rem;
		}
	}

	@media (max-width: 680px) {
		.landing-shell {
			padding: 1.5rem 1.25rem;
		}

		.landing-content {
			padding: 1.25rem 1.25rem 2rem;
		}

		.topbar {
			flex-direction: column;
			align-items: flex-start;
		}

		.nav-links {
			gap: 1rem;
		}

		.hero-copy {
			margin-bottom: 1.75rem;
		}

		.year-controls {
			gap: 0.85rem;
			flex-wrap: wrap;
		}

		.year-controls button {
			font-size: 1.15rem;
			padding: 0.45rem 0.85rem;
		}

		.card-text {
			font-size: 1rem;
		}

		.landing-footer {
			flex-direction: column;
			align-items: flex-start;
			gap: 0.9rem;
			padding: 1rem 1.25rem;
		}

		.footer-contact {
			align-items: flex-start;
			text-align: left;
		}
	}
</style>
