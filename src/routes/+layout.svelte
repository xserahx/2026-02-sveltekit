<script>
	import favicon from '$lib/assets/favicon.svg';
	import "$lib/styles/reset.css";

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />

	<link rel="preconnect" href="https://api.fontshare.com"/>
	<link href="https://api.fontshare.com/v2/css?f[]=satoshi@400,500,600,700&display=swap" rel="stylesheet"/>	
	<link href="https://api.fontshare.com/v2/css?f[]=inter@400,500,600,700&display=swap" rel="stylesheet"/>
</svelte:head>

{@render children()}
