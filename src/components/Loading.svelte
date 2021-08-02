<style>
  .loading-wrapper {
    width: 100%;
  }

  .loading-ul {
    margin: 0 auto;
    padding: 0;
    position: relative;
    background: transparent;
  }

  .dot-wrapper {
    display: block;
    position: absolute;
    top: 50%;
    left: 50%;
  }

  .dot-container {
     position: relative;
  }

  .dot {
    transform: scale(0);
    border-radius: 9999px;
  }

</style>

<script>
  export let itemCount = 14
  export let circleSize = 100
  export let itemSize = 25

  const dots = new Array(itemCount)
  const angle = (360 / itemCount)
  const rot = 0
</script>

<div
  class="loading-wrapper"
  style="height: {circleSize}px;"
>
  <ul
    class="loading-ul"
    style="width: {circleSize}px; height: {circleSize}px;"
  >
    {#each dots as dot, i}
      <li
        class="dot-wrapper"
        style="width: {itemSize}px; height: {itemSize}px; margin-top: {-itemSize / 2}px;"
      >
        <div
          class="dot-container"
          style="
            width: {itemSize}px;
            height: {itemSize}px;
            transform: rotate({(rot + (angle * (i + 1))) * 1}deg) translate({circleSize / 2}px) rotate({(rot + (angle * (i + 1))) * -1}deg);
          "
        >
          <div
            class="dot"
            style="
              background: hsl({((360 / itemCount) * i)}, 100%, 50%);
              width: {itemSize}px;
              height: {itemSize}px;
              animation: grow linear 4s {(i * (4 / itemCount))}s infinite;
            "
          >
            <!--{i}-->
          </div>
        </div>
      </li>
    {/each}
  </ul>
</div>
