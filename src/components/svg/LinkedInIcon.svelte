<style>
  svg {
    fill: var(--svg-fill);
    stroke: none;
    width: var(--svg-width);
    height: var(--svg-height);
  }
</style>

<script>
  export let cursor
</script>

<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" aria-labelledby="linkedinTitle linkedinDesc" role="img">
  <title id="linkedinTitle">LinkedIn Logo</title>
  <desc id="linkedinDesc">LinkedIn Logo in a circle</desc>
  <defs>
    <linearGradient id="grad_linkedin" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop
        offset="0%"
        style="stop-color:hsl({(cursor.x /  2)}, {cursor.y / 5}%, 50%); stop-opacity:1" />
      <stop
        offset="100%"
        style="stop-color:hsl({(cursor.x / 2) - 50}, {cursor.y / 5}%, 50%); stop-opacity:1" />
    </linearGradient>
  </defs>
  <path d="M12 0c-6.627 0-12 5.373-12 12s5.373 12 12 12 12-5.373 12-12-5.373-12-12-12zm-2 16h-2v-6h2v6zm-1-6.891c-.607 0-1.1-.496-1.1-1.109 0-.612.492-1.109 1.1-1.109s1.1.497 1.1 1.109c0 .613-.493 1.109-1.1 1.109zm8 6.891h-1.998v-2.861c0-1.881-2.002-1.722-2.002 0v2.861h-2v-6h2v1.093c.872-1.616 4-1.736 4 1.548v3.359z" fill="url(#grad_linkedin)" />
</svg>
