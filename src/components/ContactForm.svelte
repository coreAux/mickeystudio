<style>
  p {
    margin: 0 0 .25em;
    line-height: 1;
    font-weight: 400;
  }

  input,
  textarea {
    width: 100%;
    border: 1px solid rgba(0, 0, 0, .5);
    background-color: var(--input-background-color);
    border-radius: .4rem;
    box-shadow: inset 1px 1px 1px 0 rgba(0, 0, 0, .1), inset -1px -1px 1px 0 rgba(0, 0, 0, .1);
    color: var(--text-color);
    padding: .5em;
    margin-bottom: 0;
  }

  input {
    height: 3rem;
  }

  textarea {
    resize: none;
    max-height: 12rem;
  }

  input:focus,
  textarea:focus,
  button:focus {
    outline: none;
    box-shadow: 0px 0px 0 2px hotpink;
  }

  button {
    width: 100%;
    height: 3rem;
    border: none;
    background-color: var(--button-color);
    border-radius: .4rem;
    color: rgb(255, 255, 255);
    margin-top: 1rem;
    font-size: 24px;
    text-transform: uppercase;
    font-weight: 900;
    cursor: pointer;
    transition: all .5s;
    box-shadow: 0px 0px 10px 1px hotpink;
  }

  button:disabled {
    box-shadow: none;
    background-color: darkgray;
    color: gray;
    cursor: not-allowed;
  }

  label:not(first-of-type) {
    margin-top: 1rem;
  }

  .errorMessage {
    color: red;
    text-transform: uppercase;
    font-weight: 900;
  }
</style>

<script>
import Loading from "./Loading.svelte"

export let name
export let email
export let message

let sending = false
export let success
export let failed

let emailRegex = new RegExp(/^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/)

$: rowsInMessage = message.split("\n").length

let nameErrorMessage = ""
let nameError = () => {
  nameErrorMessage = name.length > 0 ? "" : "* Please enter your name."
}

let emailErrorMessage = ""
let emailError = () => {
  emailErrorMessage = emailRegex.test(email) ? "" : "* Please enter a valid email address."
}

let messageErrorMessage = ""
let messageError = () => {
  messageErrorMessage = message.length > 0 ? "" : "* Please enter a message."
}

$: sendButtonEnabled = (nameErrorMessage === "" && emailErrorMessage === "" && messageErrorMessage === "" && !!name && !!email && !!message)

function encode(data) {
  return Object.keys(data)
      .map(key => encodeURIComponent(key) + "=" + encodeURIComponent(data[key]))
      .join("&")
}

function handleSubmit(e) {
  failed = false
  sending = true
  fetch("/", {
    method: "POST",
    headers: { "Content-Type": "application/x-www-form-urlencoded" },
    body: encode({
      "form-name": e.target.getAttribute("name"),
      name,
      email,
      message
    })
  })
  .then(() => {
    sending = false
    success = true
    name = ""
    email = ""
    message = ""
    console.log("Form successfully submitted")
  })
  .catch((error) => {
    sending = false
    failed = true
    alert(error)
  })
}
</script>

{#if (!sending && !success)}
<form
  name="contact"
  data-netlify="true"
  on:submit|preventDefault={(e) => handleSubmit(e)}
>

  <input type="hidden" name="form-name" value="contact" />

<!--
<div on:click={() => (failed = !failed)} >
  Failed: {failed}
</div>
<div on:click={() => (success = !success)} >
  Success: {success}
</div>
<div on:click={() => {sending = !sending
  setTimeout(() => {sending = !sending}, 10000)}} >
  Sending: {sending}
</div>
-->

  <label>
    <p>Name</p>
    <input
      disabled={sending}
      bind:value={name}
      on:blur={nameError}
      on:input={nameError}
      type="text"
      name="name"
      style="{nameErrorMessage !== "" ? "box-shadow: 0px 0px 0 2px red;" : ""}"
    />
    <small class="errorMessage">{nameErrorMessage}</small>
  </label>

  <label>
    <p>Email</p>
    <input
      disabled={sending}
      bind:value={email}
      on:blur={emailError}
      on:input={emailError}
      type="email"
      name="email"
      style="{emailErrorMessage !== "" ? "box-shadow: 0px 0px 0 2px red;" : ""}"
    />
    <small class="errorMessage">{emailErrorMessage}</small>
  </label>

  <label>
    <p>Message</p>
    <textarea
      disabled={sending}
      bind:value={message}
      on:blur={messageError}
      on:input={messageError}
      name="message"
      rows={rowsInMessage < 4 ? 4 : rowsInMessage}
      style="{messageErrorMessage !== "" ? "box-shadow: 0px 0px 0 2px red;" : ""}"
    ></textarea>
    <small class="errorMessage">{messageErrorMessage}</small>
  </label>

  <button
    type="submit"
    disabled={sending ? true : !sendButtonEnabled}
  >
      Send
  </button>

</form>
{/if}

{#if sending}
<div style="margin-top: 3em;">
  <Loading
    itemCount={15}
    circleSize={100}
    itemSize={25}
  />
</div>
{/if}
