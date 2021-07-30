<style>
  .footer {
    display: flex;

    justify-content: space-around;
    align-items: center;
    height: 100%;
  }
</style>

<script>
import TwitterIcon from "./svg/TwitterIcon.svelte"
import LinkedInIcon from "./svg/LinkedInIcon.svelte"
import InstagramIcon from "./svg/InstagramIcon.svelte"

export let cursor
export let scrollY
export let isTouchDevice

let heightAndWidth = "50px"

$: smallScreen = isTouchDevice
</script>

<div class="footer">
  <div>
    <a href="https://www.twitter.com/hejmikael" target="_blank" rel="noreferrer">
      <TwitterIcon
        cursor={smallScreen ? {x: scrollY, y: 250} : cursor}
        --svg-fill="blue"
        --svg-height={heightAndWidth}
        --svg-width={heightAndWidth}
      />
    </a>
  </div>
  <div>
    <a href="https://www.linkedin.com/in/petersenmikael" target="_blank" rel="noreferrer">
      <LinkedInIcon
        cursor={smallScreen ? {x: scrollY - 100, y: 250} : {x: cursor.x - 100, y: cursor.y}}
        --svg-fill="blue"
        --svg-height={heightAndWidth}
        --svg-width={heightAndWidth}
      />
    </a>
  </div>
  <div>
    <a href="https://www.instagram.com/hejmikael" target="_blank" rel="noreferrer">
      <InstagramIcon
        cursor={smallScreen ? {x: scrollY - 200, y: 250} : {x: cursor.x - 200, y: cursor.y}}
        --svg-fill="blue"
        --svg-height={heightAndWidth}
        --svg-width={heightAndWidth}
      />
    </a>
  </div>
</div>
