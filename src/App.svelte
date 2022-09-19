<script>
	import RangeSlider from './RangeSlider.svelte';

	let position = 0;
	let volumePosition = 50;

	$: volumeBg = `linear-gradient(to right, #2451d7, #2451d7 ${volumePosition}%, #2451d770 ${volumePosition}%, #2451d770)`;

	function onVolumeClicked(value) {
		volumePosition += value;
	}
</script>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		font-size: 4em;
		font-weight: 100;
	}

	.container {
		margin: 10px auto;
		width: fit-content;
		text-align: center;
	}

	:global([styleContainer='sliders']) {
        width: 600px;
        padding: 10px 20px;
    }

	:global([styleTrack='demo']) {
        height: 10px;
		border-radius: 100vh;
        background: #a061b3;
    }

	:global([styleSelector='demo']) {
        width: 20px;
        height: 20px;
        background: #a061b3;
        border-radius: 100vh;
    }

	:global([styleSelector='demo']):hover {
		box-shadow: 0px 0px 0px 8px #a061b370;
    }

	.position {
		display: inline-block;
		border: thin solid;
		width: 75px;
		padding: 5px 0;
		margin-left: 10px;
		text-align: center;
	}

	.container-volume {
		margin: 0 auto;
		width: fit-content;
		display: flex;
		flex-direction: row;
	}

	.container-volume span {
		cursor: pointer;
		caret-color: transparent;
		user-select: none;
	}

	:global([styleTrack='volume']) {
        height: 6px;
        background: #2451d7;
    }

	:global([styleSelector='volume']) {
        width: 15px;
        height: 20px;
        background: #2451d7;
    }

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>

<svelte:head>
    <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons" />
</svelte:head>

<main>
	<h1>Svelte Range Slider</h1>
	<div class="container">
		<RangeSlider bind:position styleContainer="sliders" styleTrack="demo" styleSelector="demo" />
		<span class="position">{position.toFixed(2)}</span>
	</div>
	<div class="container-volume">
		<span class="material-icons" on:click={() => onVolumeClicked(-5)}>volume_mute</span>
		<RangeSlider bind:position={volumePosition} styleContainer="sliders" styleTrack="volume" styleSelector="volume" background={volumeBg} />
		<span class="material-icons" on:click={() => onVolumeClicked(5)}>volume_up</span>
	</div>
</main>
