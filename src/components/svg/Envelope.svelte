<style>
  @keyframes cradle {
    0% {
      transform: rotate(25deg) scale(.8);
    }
    100% {
      transform: rotate(-25deg) scale(1.2);
    }
  }

  svg {
    /* animation: cradle ease-in-out 3s alternate infinite; */
    transform: rotate(-25deg);
  }

  path {
    fill: var(--text-color);
  }
</style>


<svg width="50" height="50" viewBox="0 0 50 50" fill="none" xmlns="http://www.w3.org/2000/svg">
  <path fill-rule="evenodd" clip-rule="evenodd" d="M48.2296 10.6785C47.5925 10.25 46.8255 10 46 10H4C3.34288 10 2.72277 10.1585 2.17579 10.4392L21.7868 30.0502C23.7394 32.0029 26.9052 32.0029 28.8579 30.0502L48.2296 10.6785ZM48.985 11.3373L29.565 30.7574C27.2218 33.1005 23.4228 33.1005 21.0797 30.7574L1.33731 11.015C0.516668 11.7475 0 12.8134 0 14V36C0 38.2091 1.79086 40 4 40H46C48.2091 40 50 38.2091 50 36V14C50 12.9774 49.6163 12.0445 48.985 11.3373ZM16 27L2 38L1.38218 37.2137L15.3822 26.2137L16 27ZM48 38L34.3181 27.2499L34.9359 26.4636L48.6178 37.2137L48 38Z" fill="black"/>
</svg>
