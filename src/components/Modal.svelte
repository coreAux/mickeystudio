<style>
  .modal-background {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, .2);
    background: linear-gradient(90deg, rgba(255, 0, 0, .8), rgba(255, 0, 255, .8)), linear-gradient(180deg, rgba(0, 0, 0, .8), rgba(255, 255, 0, .8));
    background-blend-mode: exclusion;
    z-index: 99;
  }

  .modal-wrapper {
    position: absolute;
    top: 50%;
    left: 50%;
    width: calc(420px + 50px + 50px);
    height: 90vh;
    background: transparent;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 100;
    transform: translate(-50%, -50%);
  }

  .modal {
    background-color: var(--background-color);
    width: 420px;
    min-height: 75vh;
    border-radius: 3rem;
    z-index: 101;
    padding: 1em 1em 2em;
    align-self: flex-start;
    box-shadow: 5px 5px 5px 0 rgba(0, 0, 0, .2);
  }

  .close-button {
    margin-left: 1rem;
    width: 50px;
    height: 50px;
    align-self: flex-start;
    border-radius: 9999px;
    background-color: transparent;
    position: relative;
    z-index: 101;
    cursor: pointer;
  }

  .close-button:focus {
    outline: none;
    box-shadow: 0px 0px 0 2px hotpink;
  }

  @media (max-width: 700px) {
    .modal-wrapper {
      width: 100vw;
      height: 100vh;
    }

    .modal {
      margin-top: 1em;
      min-height: 90vh;
      /* height: 90vh; */
    }

    .close-button {
      position: absolute;
      top: 2em;
      right: calc((100vw - 420px) / 2);
    }
  }

  @media (max-width: 445px) {
    .close-button {
      right: 1em;
    }
  }
</style>

<script>
  import CloseButton from "./svg/CloseButton.svelte"
  export let toggleModal

  let counter = 0
  let hue = 0
  let timer = setInterval(() => {
    counter += 1
    hue = Math.sin(counter * 0.005) * 360
  }, 1000)

  function handleKeyDown() {
    if (event.key === "Tab" || event.key === "Shift") {
      console.log(event.key)
    } else {
      toggleModal()
    }
  }
</script>

<div
  on:click={toggleModal}
  style="background: linear-gradient(90deg, hsla({hue}, 100%, 50%, .8), hsla({hue + 300}, 100%, 50%, .8)), linear-gradient(180deg, rgba(0, 0, 0, .8), rgba(255, 255, 0, .8));"
  class="modal-background"
>
</div>

<div
  class="modal-wrapper"
>
  <div class="modal">
    <slot name="header">
      Modal
    </slot>

    <slot name="copy">
      Hi! You've opened the modal, but there's nothing here to see right now.
    </slot>

    <slot name="component" />
  </div>
  <div
    on:click={toggleModal}
    on:keydown={handleKeyDown}
    tabindex=0
    class="close-button"
  >
    <CloseButton />
  </div>
</div>
