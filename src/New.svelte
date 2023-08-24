<script>
  let title = "";
  let description = "";
  let markdown = "";
  let post = null;
  let files;
  let img;
  let number = 2;
  console.log(number);
  async function submitPost() {
    try {
      post = {
        title: title,
        description: description,
        markdown: markdown,
        image: img,
      };
      const response = await fetch("http://localhost:3000/post", {
        method: "POST",
        body: JSON.stringify(post),
        headers: {
          "Content-Type": "application/json",
        },
      });
      if (response.ok) {
        console.log("Post Submitted Successfully");
      } else {
        console.error("Failed to submit post");
      }
    } catch (error) {
      console.error("Error sending data:", error);
    }
  }
  function getURL(url) {
    img = url;
  }
</script>
<main>
  <nav class="navbar navbar-light bg-light">
    <a class="navbar-brand" href="/">
      <img src="/assets/112121.jpg" width="30" height="30" alt="" />
      Sports Blog
    </a>
  </nav>
  <div class="container">
    <h1 class="mb-4">New Article</h1>
    <form>
      <div class="form-group">
        <label for="title">Title</label>
        <input
          required
          bind:value={title}
          type="text"
          name="title"
          id="title"
          class="form-control"
        />
      </div>
      <div class="form-group">
        <label for="description">Description</label>
        <textarea
          name="description"
          id="description"
          bind:value={description}
          class="form-control"
        />
      </div>
      <div class="form-group">
        <label for="markdown">Markdown</label>
        <textarea
          required
          name="markdown"
          id="markdown"
          bind:value={markdown}
          class="form-control"
        />
      </div>
    </form>
    <a href="/">
      <button on:click={submitPost} class="btn btn-primary mt-4"> Save </button>
    </a>
    <a href="/" class="btn btn-secondary mt-4">Cancel</a>
    <div>
      <input id="chooseFile" type="file" bind:files />
      {#if files && files[0]}
        <p>
          <img src={URL.createObjectURL(files[0])} alt="A Pic" />
          {getURL(URL.createObjectURL(files[0]))}
          {console.log(URL.createObjectURL(files[0]))}
        </p>
      {/if}
    </div>
  </div>
</main>
