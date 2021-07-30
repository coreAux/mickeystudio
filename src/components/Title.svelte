<style>
	@keyframes test {
		0%, 100% {
			transform: scaleY(1);
		}
		50% {
			transform: scaleY(.2);
		}
	}

	h1 {
		font-size: 5rem;
    display: inline-block;
		margin-left: 10rem;
  }

  .titleLetter {
		animation: test 1s ease-in-out infinite;
	}

	@media (max-width: 700px) {
		h1 {
			font-size: 4rem;
			margin-left: 0;
		}
	}

</style>

<script>
	export let cursor
	export let windowInnerWidth
	export let smallBreakPoint
	export let isTouchDevice

	let counter = 0
	let hue = 0
	let timer = setInterval(() => {
		counter += 1
		hue = Math.sin(counter * 0.005) * 360
	}, 100)

	let mickey = ["M", "I", "C", "K", "E", "Y"]
</script>

{#if (windowInnerWidth > smallBreakPoint || !isTouchDevice)}
	<h1>
	{#each mickey as letter, i}
		<span
			class="titleLetter"
			style="
				 display: inline-block;
				 color: hsl({(cursor.x / 2) - (i * 10)}, {cursor.y / 5}%, 50%);
				 {cursor.x > i * (windowInnerWidth / mickey.length) && cursor.x < i * (windowInnerWidth / mickey.length) + (windowInnerWidth / mickey.length) ? "animation-play-state: play;" : "animation-play-state: paused;"}
			 "
		>
			{letter}
		</span>
	{/each}
	</h1>
{:else}
	<h1>
	{#each mickey as letter, i}
		<span
			class="titleLetter"
			style="
				 display: inline-block;
				 color: hsl({hue - (i * 10)}, 50%, 50%);
				 animation-play-state: paused;
			 "
		>
			{letter}
		</span>
	{/each}
	</h1>
{/if}
<!--<small>.STUDIO</small>-->
