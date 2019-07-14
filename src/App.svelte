<script>
  import { onMount, afterUpdate } from "svelte";

  let error = false;

  let text = "";
  let textareaElement;

  $: letters = text.length - 1;
  $: textArray = text.length === 0 ? [] : text.toLowerCase().split("");

  const original =
    "Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.";
  const originalArray = original.toLowerCase().split("");

  onMount(() => {
    textareaElement.focus();
  });

  afterUpdate(() => {
    if (textareaElement && document.activeElement.tagName !== "TEXTAREA") {
      textareaElement.focus();
    }
  });

  function handleKeyUp() {
    const updatedArray = [...originalArray];
    updatedArray.length = textArray.length;

    if (JSON.stringify(textArray) !== JSON.stringify(updatedArray)) {
      error = true;
    }
  }

  function handleRetry() {
    error = false;
    text = "";
    window.scrollTo(0, 0);
  }
</script>

<style>
  .original {
    position: relative;
    font-size: 60px;
    line-height: 1.2;
    margin: 0;
  }

  .original p {
    margin: 0;
  }

  .try {
    position: absolute;
    margin: 0;
    top: 0;
    left: 0;
    width: 100%;
    color: red;
  }

  textarea {
    font-size: 60px;
    line-height: 1.2;
    width: 100%;
    resize: none;
  }

  button {
    background-color: transparent;
    outline: none;
    font-weight: bold;
    font-size: 34px;
    margin: 40px 0 0;
    padding: 10px 20px 13px;
    cursor: pointer;
    border: 4px dashed red;
    color: red;
  }

  button:hover {
    border: 4px solid red;
  }

  span {
    position: relative;
    padding: 10px 15px;
    border: 4px dashed red;
    color: red;
    font-weight: bold;
    transform: rotate(2deg);
    display: inline-block;
  }
</style>

{#if error}
  <p>
    Snap, you failed!
    <span>You achieved {letters} {letters === 1 ? 'letter' : 'letters'}.</span>
  </p>
  <div class="original">
    <p>{original.toLowerCase()}</p>
    <p class="try">{text.toLowerCase()}</p>
  </div>
  <button on:click={() => handleRetry()}>Retry</button>
{:else}
  <p>
    Try to type the
    <span>Lorem ipsum</span>
    text. Let´s see how far you can get:
  </p>
  <textarea
    bind:value={text}
    bind:this={textareaElement}
    placeholder="..."
    on:keyup={() => handleKeyUp()} />
{/if}
