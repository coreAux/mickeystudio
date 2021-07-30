<style>
	div {
		width: 300px;
		height: 300px;
    /* border-radius: 9999px; */
	}

	.card {
		-webkit-transform-style: preserve-3d;
	  transform-style: preserve-3d;
  	transition: all .5s ease-in-out;
	}

	.face {
		position: absolute;
    top: 0;
    left: 0;
		width: 100%;
		height: 100%;
		-webkit-backface-visibility: hidden;
	  backface-visibility: hidden;
	  background-color: whitesmoke;
	}

	.back {
		z-index: -1;
		background-color: gray;
		-webkit-transform: rotateY(180deg);
	  transform: rotateY(180deg);

		overflow:hidden;
	  display: block;
	}

	.hovercard:hover > div.card {
  	-webkit-transform: rotateY(180deg);
	  transform: rotateY(180deg);
	}

	.hovercard {
		background: transparent;
		margin-left: auto;
		margin-right: auto;
	}

	.front, .back {
    border-radius: 9999px;
	}

	.front {
		z-index: 1;
	}

	@media (max-width: 700px) {
		.hovercard:hover > div.card {
			-webkit-transform: unset;
			transform: unset;
		}
	}
</style>

<script>
export let windowInnerWidth
export let smallBreakPoint
export let scrollY

let container
let card
$: containerRect = container && container.getBoundingClientRect()

$: if (windowInnerWidth < smallBreakPoint) {
	if (scrollY > (containerRect.top / 2)) {
		card.style = "transform: rotateY(180deg);"
	} else {
		card.style = ""
	}
}
</script>

<div
	class="hovercard"
	bind:this={container}
>
	<div
		class="card"
		bind:this={card}
	>
		<img src="https://www.mikaelpetersen.se/static/b0c6b243b669729ed0acd9470c008e13/6d09e/profile-photo-bw.webp" alt="Mickey" class="front face" height="300" width="300" />
		<img src="https://www.mikaelpetersen.se/static/c909efd23a09babd71b159279b387e79/6d09e/profile-photo.webp" alt="Mickey" class="back face" height="300" width="300" />
	</div>
</div>
