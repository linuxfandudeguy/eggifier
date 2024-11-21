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
    margin-top: 40px;
    padding: 10px 0;
    background-color: #f8f9fa;
  }

  footer a {
    text-decoration: none;
    color: #007bff;
    font-weight: bold;
  }

  footer a:hover {
    color: #0056b3;
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

  <footer>
    <a href="https://lelbois.wordpress.com/2024/11/21/eggifier-eggify-your-sentences/" target="_blank" rel="noopener noreferrer">Read the article</a>
  </footer>
</div>
