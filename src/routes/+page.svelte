<script>
  import nlp from 'compromise';

  let sentence = '';
  let result = '';

  function escapeHTML(str) {
    const div = document.createElement('div');
    div.textContent = str;
    return div.innerHTML;
  }

  function eggify() {
    console.log("eggified");
    let modifiedSentence = sentence;
    const doc = nlp(sentence);

    // Replace every noun with the word "egg", maintaining case
    doc.nouns().forEach(noun => {
      const nounText = noun.text();

      if (nounText === nounText.toUpperCase()) {
        modifiedSentence = modifiedSentence.replace(nounText, "EGG"); // Uppercase
      } else if (nounText === nounText.toLowerCase()) {
        modifiedSentence = modifiedSentence.replace(nounText, "egg"); // Lowercase
      } else if (nounText[0] === nounText[0].toUpperCase()) {
        modifiedSentence = modifiedSentence.replace(nounText, "Egg"); // Titlecase
      }
    });

    result = escapeHTML(modifiedSentence); // Escape before rendering
  }
</script>

<style>
  @import './app.css';

  .container {
    max-width: 600px;
    margin: 0 auto;
    padding-top: 50px;
    padding-bottom: 60px; /* To ensure there's space for footer */
    min-height: 100vh;
  }

  h1 {
    text-align: center;
  }

  .form-group {
    margin-bottom: 20px;
  }

  .btn {
    width: 100%;
  }

  footer {
    text-align: center;
    margin-top: auto; /* Pushes the footer to the bottom */
    padding: 10px 0;
    background-color: #f8f9fa;
    font-size: 12px; /* Smaller text */
  }

  footer a {
    text-decoration: none;
    color: #007bff;
    font-weight: bold;
  }

  footer a:hover {
    color: #0056b3;
  }

  /* Overlay for No JavaScript */
  .no-js-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.7);
    color: white;
    font-size: 24px;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }

  .no-js-message {
    text-align: center;
  }
</style>

<div class="container">
  <h1>Eggify Your Sentences! 🥚</h1>

  <div class="form-group">
    <label for="sentenceInput">Enter a sentence</label>
    <input
      type="text"
      id="sentenceInput"
      class="form-control"
      bind:value={sentence}
      placeholder="Type a sentence here"
    />
  </div>

  <button class="btn btn-primary" on:click={eggify}>Eggify!</button>

  {#if result}
    <div class="mt-3">
      <h3>Processed Sentence:</h3>
      <p>{result}</p>
    </div>
  {/if}
</div>

<!-- No JavaScript message for browsers with JS disabled -->
<noscript>
  <div class="no-js-overlay">
    <div class="no-js-message">
      <p>This application cannot work without JavaScript. Please enable JavaScript to use it.</p>
    </div>
  </div>
</noscript>
