<style>
	main {
		overflow: auto;
		margin: 0 auto;
		padding: 1em 0;
		display: grid;
		grid-template-columns: 75vw auto;
		grid-template-rows: 10vh auto 10vh;
	}

	main.modal-open {
		overflow: hidden;
		position: fixed;
		left: 0px;
		padding: 1rem 2rem;
	}

	.title-wrapper {
		/* border: 1px solid rgba(0, 0, 255, 1); */
		grid-column-start: 1;
		grid-column-end: span 1;
		grid-row-start: 1;
		grid-row-end: span 1;
		justify-self: start;
		align-self: center;
	}

	.theme-toggler-wrapper {
		/* border: 1px solid rgba(255, 0, 0, 1); */
		grid-column-start: 2;
		grid-column-end: span 1;
		grid-row-start: 1;
		grid-row-end: span 1;
		justify-self: center;
		align-self: center;
	}

	.body-wrapper {
		/* border: 1px solid rgba(0, 255, 255, 1); */
		grid-column-start: 1;
		grid-column-end: span 2;
		grid-row-start: 2;
		grid-row-end: span 1;
	}

	.profile-photo-wrapper {
		float: right;
		margin: 1em;
		shape-outside: circle(50%);
	}

	.contact-button-wrapper {
		float: left;
		shape-outside: circle(50%);
		margin: 1em;
		cursor: pointer;
		border: 1px solid hotpink;
		box-shadow: 0px 0px 10px 1px hotpink;
		border-radius: 9999px;
		width: 100px;
		display: grid;
		place-items: center center;
	}

	.contact-button-wrapper > div {
		grid-area: 1 / 1;
	}

	.footer-wrapper {
		/* border: 1px solid rgba(255, 0, 255, 1); */
		grid-column-start: 1;
		grid-column-end: span 2;
		grid-row-start: 3;
		grid-row-end: span 3;
	}

/*  .stuffs {
		position: sticky;
		width: 200px;
		margin-left: auto;
		margin-right: 10px;
		bottom: 10px;
		opacity: .5;
		background-color: var(--text-color);
		color: var(--background-color);
		border-radius: .4em;
		font-size: 12px;
		padding: .5em;
		z-index: 999;
	}*/

	p {
		font-size: 24px;
	}

	.emoji {
		text-shadow: 1px 1px 2px rgba(0, 0, 0, .1), -1px -1px 2px rgba(0, 0, 0, .1);
	}

	@media (max-width: 700px) {
		main {
			padding-bottom: 2em;
		}

		main.modal-open {
			padding: 1rem;
		}

		.profile-photo-wrapper {
			float: none;
			margin: 2rem 0;
		}

		p {
			text-align: center;
		}
	}
</style>

<script>
	import Title from "./components/Title.svelte"
	import ThemeToggler from "./components/ThemeToggler.svelte"
	import ProfilePhoto from "./components/ProfilePhoto.svelte"
	import Footer from "./components/Footer.svelte"
	import ContactForm from "./components/ContactForm.svelte"
	import Modal from "./components/Modal.svelte"
	import ContactButton from "./components/svg/ContactButton.svelte"
	import Envelope from "./components/svg/Envelope.svelte"

	let windowInnerWidth
	let windowInnerHeight
	let scrollY
	let cursor = { x: 0, y: 0 }
	let smallBreakPoint = 700

	let showModal = false

	// ContactForm stuffs
	let name = ""
	let email = ""
	let message = ""

	let success = false
	let failed = false

	function handleMousemove(event) {
		cursor.x = event.clientX
		cursor.y = event.clientY
	}

	let top = 0

	function resetMessage() {
		success = false
		failed = false
	}

	function toggleModal() {
		resetMessage()
		showModal = !showModal
		document.body.classList.toggle("modal-open")

		if (showModal) {
			top = scrollY
		}
	}

	$: if (!showModal) {
		setTimeout(() => {
			window.scroll(0, top)
		}, 100)
	}

	let isTouchDevice = (('ontouchstart' in window) || (navigator.maxTouchPoints > 0) || (navigator.msMaxTouchPoints > 0))
/*	console.log('ontouchstart' in window)
	console.log(navigator.maxTouchPoints > 0)
	console.log(navigator.msMaxTouchPoints > 0)*/
</script>

<svelte:head>
	<meta name="description" content="This is a site about Mickey, lawyer and web developer!" />
  <meta name="theme-color" content="#85baa1" />
	<link rel="manifest" href="manifest.json" />
  <link rel="apple-touch-icon" href="favicon192x192.png" />
</svelte:head>

<svelte:body
	on:mousemove={handleMousemove}
	on:mouseleave={() => cursor = {x: 0, y: 0}}
/>
<svelte:window
	bind:innerWidth={windowInnerWidth}
	bind:innerHeight={windowInnerHeight}
	bind:scrollY={scrollY}
/>

{#if showModal}
	<Modal
		bind:success={success}
		bind:failed={failed}
		toggleModal={toggleModal}
	>
		<h2 slot="header">Contact me</h2>
		<p slot="copy">

			{#if !success && !failed}
				Send me a message! <span class="emoji" role="img" aria-label="Closed Letterbox with Raised Flag" >📫</span>
			{:else if !success && failed}
				Something went wrong <span class="emoji" role="img" aria-label="Face with Raised Eyebrow" >🤨</span><br />
				Please try again later.
			{:else if success && !failed}
				Thanks for your message! <span class="emoji" role="img" aria-label="Party Face" >🥳</span><br />
				I'll get back to you as soon as possible.
			{/if}

		</p>
		<ContactForm
			slot="component"
			bind:success={success}
			bind:failed={failed}
			bind:name={name}
			bind:email={email}
			bind:message={message}
		/>
	</Modal>
{/if}

<main
	class="{showModal ? "modal-open" : "modal-closed"}"
	style="top: {showModal ? -top : scrollY}px;"
>
	<div class="title-wrapper">
		<Title
			cursor={cursor}
			windowInnerWidth={windowInnerWidth}
			smallBreakPoint={smallBreakPoint}
			isTouchDevice={isTouchDevice}
		/>
	</div>
	<div class="theme-toggler-wrapper">
		<ThemeToggler />
	</div>
	<div class="body-wrapper">
		<div class="profile-photo-wrapper">
			<ProfilePhoto
				windowInnerWidth={windowInnerWidth}
				smallBreakPoint={smallBreakPoint}
				isTouchDevice={isTouchDevice}
				scrollY={scrollY}
			/>
		</div>

		<!-- <p>Hi, I'm Mickey! I'm a Digital Program Manager at one of Sweden's larger law firms. I have a law degree (LL.M.) from Stockholm University, I've done a few courses with <a href="https://www.superhi.com/?r=Micke" target="_blank" rel="noreferrer"><span class="uppercase clip-to-text">SuperHi</span></a> (check them out - they're great!) and is currently studying an online full stack JavaScript-course at the University of Helsinki.</p> -->

		<p>Hi! My name is Mickey and I enjoy making interactive and colorful websites <span class="emoji" role="img" aria-label="Laptop">💻. In need of a custom made website? Send me a message <span class="emoji" role="img" aria-label="Envelope">✉️ and let's talk!</p>

		<div
			class="contact-button-wrapper"
			on:click={toggleModal}
			style="
				border: 1px solid hsl({isTouchDevice ? scrollY : (cursor.x / 2)}, {isTouchDevice ? "250" : (cursor.y / 5)}%, 50%);
				box-shadow: 0px 0px 10px 1px hsl({isTouchDevice ? scrollY : (cursor.x / 2)}, {isTouchDevice ? "250" : (cursor.y / 5)}%, 50%);
			"
		>
			<div
				style="display: flex; align-items: center; justify-content: center;"
			>
				<ContactButton />
			</div>
			<div>
				<Envelope />
			</div>
		</div>

		<p>I've lived for the majority of my life in Sweden 🇸🇪. Recently me and my boyfriend <span class="emoji" role="img" aria-label="Men Holding Hands" >👨🏻‍🤝‍👨🏼</span> decided to change things up and we now live in Amsterdam <span class="emoji" role="img" aria-label="Flag of Netherlands">🇳🇱!</p>

		<p>I have a law degree (LL.M.)<span class="emoji" role="img" aria-label="Graduation Cap">🎓</span> and I have worked in the law industry for the majority of my adult life. I'm also a skilled front-end web developer and spend most of my free time coding. I'm well-versed with HTML, CSS and JavaScript, and libraries such as React and Svelte.</p>
	</div>
	<div class="footer-wrapper">
		<Footer
			cursor={cursor}
			scrollY={scrollY}
			isTouchDevice={isTouchDevice}
		/>
	</div>
</main>

<!--
<div class="stuffs">
	Cursor X: {cursor.x}<br/>
	Cursor Y: {cursor.y}<br/>
	Window Inner Width: {windowInnerWidth}<br/>
	Window Inner Height: {windowInnerHeight}<br/>
	Scroll Y : {scrollY}
	Top: {top}
</div>
-->
