<script>
  import { onMount, afterUpdate } from "svelte";

  let error = false;
  let pasteError = false;

  let text = "";
  let textareaElement;

  $: letters = text.length - 1;
  $: textArray = text.length === 0 ? [] : text.toLowerCase().split("");

  const original =
    "Lorem ipsum dolor sit amet, consectetur adipisici elit, sed eiusmod tempor incidunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquid ex ea commodi consequat. Quis aute iure reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint obcaecat cupiditat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi. Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi. Nam liber tempor cum soluta nobis eleifend option congue nihil imperdiet doming id quod mazim placerat facer possim assum. Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, At accusam aliquyam diam diam dolore dolores duo eirmod eos erat, et nonumy sed tempor et et invidunt justo labore Stet clita ea et gubergren, kasd magna no rebum. sanctus sea sed takimata ut vero voluptua. est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat. Consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.";
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

  function handlePaste() {
    pasteError = true;
  }

  function handleRetry() {
    pasteError = false;
    error = false;
    text = "";
    window.scrollTo(0, 0);
  }
</script>

<style>
  .original,
  textarea {
    position: relative;
    font-size: 40px;
    line-height: 1.2;
    margin: -9px 0 0;
    padding: 10px 20px 13px;
    height: 50vh;
    overflow-y: auto;
    border: 4px dashed red;
  }

  .flag {
    font-size: 10px;
    text-transform: uppercase;
    padding: 5px;
    background: red;
    color: #fff;
    margin: 0;
    display: inline-block;
  }

  .original p {
    margin: 0;
  }

  .try {
    position: absolute;
    margin: 0;
    top: 0;
    left: 0;
    width: calc(100% - 40px);
    padding: 10px 20px 13px;
    color: red;
  }

  button {
    background-color: transparent;
    outline: none;
    font-weight: bold;
    font-size: 34px;
    margin: 0;
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
    display: inline-block;
    transform: rotate(2deg);
  }

  .sharing {
    display: flex;
    align-items: center;
  }

  .sharing p {
    flex-grow: 2;
  }
  .sharing button {
    margin: 20px 0 20px 20px;
  }

  .credits {
    color: red;
    font-size: 10px;
    letter-spacing: 0.02em;
    text-align: right;
    text-transform: uppercase;
    font-weight: bold;
    margin: 2px 0;
  }

  .credits a {
    text-decoration: underline;
    border: none;
  }
</style>

{#if error}
  <p>
    Snap, you failed!
    <span>You achieved {letters} {letters === 1 ? 'letter' : 'letters'}.</span>
  </p>

  <p class="flag">Original Text</p>
  <div class="original">
    <p>{original.toLowerCase()}</p>
    <p class="try">{text.toLowerCase()}</p>
  </div>
  <div class="sharing">
    <p>
      Share on
      <a
        target="_blank"
        rel="noopener noreferrer"
        href={`http://twitter.com/share?text=I achieved ${letters} ${letters === 1 ? 'letter' : 'letters'} of the 'lorem ipsum' text. How many can you achieve?&url=http://loremipsumgame.netlify.com&hashtags=loremipsum,game`}>
        Twitter
      </a>
      or
      <a
        href="https://www.facebook.com/sharer/sharer.php?u=http://loremipsumgame.netlify.com"
        target="_blank">
        Facebook
      </a>

    </p>
    <button on:click={() => handleRetry()}>Retry</button>
  </div>
{:else if pasteError}
  <p>
    Hey, that is not fair!
    <span>Do not copy and paste!</span>
  </p>
  <button on:click={() => handleRetry()}>Retry</button>
{:else}
  <p>
    Try to type the
    <span>Lorem ipsum</span>
    text. Let´s see how far you can get:
  </p>
  <p class="flag">Your try</p>
  <textarea
    bind:value={text}
    bind:this={textareaElement}
    placeholder="..."
    autocomplete="off"
    autocorrect="off"
    autocapitalize="off"
    spellcheck="false"
    on:paste={() => handlePaste()}
    on:keyup={() => handleKeyUp()} />
  <p class="credits">
    Made with ♥ by
    <a
      href="https://github.com/jeslage"
      target="_blank"
      rel="noopener noreferrer">
      Johannes Eslage
    </a>
  </p>
{/if}
