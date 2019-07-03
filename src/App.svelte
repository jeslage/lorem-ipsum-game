<script>
  let error = false;

  let text = "";

  $: letters = text.length - 1;
  $: textArray = text.length === 0 ? [] : text.toLowerCase().split("");

  const original =
    "Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.";
  const originalArray = original.toLowerCase().split("");

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
  }
</script>

<style>
  .lorem__original {
    position: relative;
    margin: 0;
  }

  .lorem__try {
    position: absolute;
    margin: 0;
    top: 0;
    left: 0;
    width: 100%;
    color: red;
  }

  textarea {
    font-size: 60px;
    width: 100%;
    resize: none;
  }
</style>

{#if error}
  <p>
    Snap, you failed! You achieved {letters} {letters === 1 ? 'letter' : 'letters'}.
  </p>
  <p>This is what you got:</p>
  <div class="lorem__original">
    <p>{original.toLowerCase()}</p>
    <p class="lorem__try">{text.toLowerCase()}</p>
  </div>
  <button on:click={() => handleRetry()}>Retry</button>

{:else}
  <textarea
    bind:value={text}
    placeholder="Lorem ipsum..."
    on:keyup={() => handleKeyUp()} />
{/if}
