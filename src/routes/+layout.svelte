<script lang="ts">
	import '../app.css';
	import { ModeWatcher } from "mode-watcher";
    import Countdown from './Countdown.svelte';
	let { children } = $props();
</script>

<svelte:head>
	<title>New Year Countdown 2025</title>
	<meta property="og:image" content="./meta-2025.jpg">
	<meta property="og:image:width" content="1200">
	<meta property="og:image:height" content="630">
</svelte:head>
<ModeWatcher />
{@render children()}
