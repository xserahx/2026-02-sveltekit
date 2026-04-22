<script>
	// import favicon from '$lib/assets/favicon.svg';
	import "$lib/styles/reset.css";
	import "$lib/styles/tokens.css";
	import "$lib/styles/global.css";

	let { children } = $props();
</script>

<svelte:head>
	<title>Days of Serah</title>
	<link rel="icon" type="image/svg+xml" href="/favicon.svg" />

	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,opsz,wght@0,6..96,400..900;1,6..96,400..900&family=Outfit:wght@100..900&display=swap" rel="stylesheet" />
</svelte:head>

{@render children()}
