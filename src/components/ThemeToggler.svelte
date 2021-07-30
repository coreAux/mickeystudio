<style>
  .switch {
    width: 50px;
    height: 24px;
    border-radius: 9999px;
    background-color: var(--switch-background-color);
    border: 1px solid rgba(0, 0, 0, .5);
    box-shadow: inset 1px 1px 1px 0 rgba(0, 0, 0, .1), inset -1px -1px 1px 0 rgba(0, 0, 0, .1);
    position: relative;
    display: grid;
    grid-template-columns: 50% 50%;
    cursor: pointer;
  }

  .moon {
    background-color: transparent;
  }

  .sun {
    background-color: transparent;
  }

  .button {
    width: 22px;
    height: 22px;
    border-radius: 9999px;
    background-color: var(--switch-button-color);
    position: absolute;
    top: 1px;
    left: 1px;
    transition: transform .3s, background-color .1s;
    box-shadow: 1px 1px 1px 0 rgba(0, 0, 0, .1);
  }

  .button:focus {
    outline: none;
    box-shadow: 0px 0px 0 2px hotpink;
  }

  .button.left {
    transform: translateX(26px);
    z-index: 1;
  }
</style>

<script>
  import { onMount } from 'svelte';

  let darkmode = (!!window.matchMedia && window.matchMedia("(prefers-color-scheme: dark)").matches)

  onMount(() => {
    darkmode ? document.documentElement.classList.toggle("darkmode") : ""
  })

	function handleClick() {
    if (event.key === "Tab" || event.key === "Shift") {
      console.log("TAB!")
    } else {
      darkmode = !darkmode
      document.documentElement.classList.toggle("darkmode")
    }
	}
</script>

<div
  on:click={handleClick}
  class="switch"
>
  <div
    class="moon"
  >

  </div>
  <div
    class="sun"
  >

  </div>
  <div
    tabindex=0
    on:keydown={handleClick}
    class="button {darkmode ? "left" : "right"}"
    style="background-position: {darkmode ? "100%" : "0%"} 0%; {darkmode ? "background: linear-gradient(0deg, rgba(15, 2, 222), rgb(245, 2, 253));" : "background: linear-gradient(0deg, red, yellow);"}"
  />
  <!--  -->
</div>
