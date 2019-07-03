<script>
  let error = false;

  let text = "";

  $: letters = text.length - 1;
  $: textArray = text.length === 0 ? [] : text.toLowerCase().split("");

  const original =
    "Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.";
  const originalArray = original.toLowerCase().split("");

  function handleKeyUp() {
    console.log("up");
    const updatedArray = [...originalArray];
    updatedArray.length = textArray.length;
    console.log(textArray);
    if (JSON.stringify(textArray) !== JSON.stringify(updatedArray)) {
      error = true;
    }
  }

  function handleRetry() {
    error = false;
    text = "";
  }
</script>

{#if error}
  <p>Snap, you failed!</p>
  <p>You achieved {letters} letters.</p>
  <button on:click={() => handleRetry()}>Retry</button>
{:else}
  <textarea
    bind:value={text}
    placeholder="Lorem ipsum..."
    on:keyup={() => handleKeyUp()} />
{/if}
