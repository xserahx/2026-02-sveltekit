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
	<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+Display:ital,wght@0,400;0,500;0,600;0,700;0,800;0,900;1,400;1,500;1,600;1,700;1,800;1,900&family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap" rel="stylesheet" />
</svelte:head>

{@render children()}
