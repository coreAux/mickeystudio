<style>
  @keyframes rotate {
    0% {
      transform: rotate(360deg);
    }
    100% {
      transform: rotate(0deg);
    }
  }

  svg {
    width: 100px;
    height: 100px;
    border-radius: 9999px;
    background-color: transparent;
    animation: rotate linear 60s infinite;
  }

  textPath {
    font-size: 12px;
    letter-spacing: .4px;
    font-weight: 900;
    text-transform: uppercase;
    fill: var(--text-color);
    /*text-shadow:
      0 0 7px hotpink,
      0 0 10px hotpink,
      0 0 21px hotpink,
      0 0 42px hotpink,
      0 0 82px #0fa,
      0 0 92px #0fa,
      0 0 102px #0fa,
      0 0 151px #0fa*/;
  }
</style>

<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
	<defs>

    <path id="MyPath" d="M5,50a45,45 0 1,0 90,0a45,45 0 1,0 -90,0" />
	</defs>
	<text>
		<textPath href="#MyPath" side="right">
			Send me a message – Send me a message –
		</textPath>
	</text>
</svg>


<!-- <circle id="MyPath" cx="50" cy="50" r="39"/> -->
