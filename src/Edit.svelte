<script>
  let url = window.location.href;
  url = url.split("/");
  let id = url[5];
  let post;
  async function fetchData() {
    let link = "http://localhost:3000/post/edit/";
    let res = link.concat(id);
    try {
      const response = await fetch(res);
      if (!response.ok) {
        throw new Error("Network response was not ok");
      }
      post = await response.json();
      post = post.itemData;
      console.log(post);
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  }
  async function submitPost() {
    let link = "http://localhost:3000/post/edit/";
    let res = link.concat(id);
    console.log(post.title);
    fetch(res, {
      method: "PUT",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        title: post.title,
        description: post.description,
        markdown: post.markdown,
      }),
    })
      .then((response) => response.json())
      .then((result) => console.log(result));
  }
</script>
<main>
  <nav class="navbar navbar-light bg-light">
    <a class="navbar-brand" href="/">
      <img src="/assets/112121.jpg" width="30" height="30" alt="" />
      Sports Blog
    </a>
  </nav>
  {#await fetchData() then}
    <div class="container">
      <h1 class="mb-4 mt-3">Edit Article</h1>
      <form>
        <div class="form-group">
          <label id="title" for="title">Title</label>
          <input
            required
            bind:value={post.title}
            type="text"
            name="title"
            id="title"
            class="form-control"
          />
        </div>
        <div class="form-group">
          <label id="description" for="description">Description</label>
          <textarea
            name="description"
            id="description"
            bind:value={post.description}
            class="form-control"
          />
        </div>

        <div class="form-group">
          <label id="markdown" for="markdown">Markdown</label>
          <textarea
            required
            name="markdown"
            id="markdown"
            bind:value={post.markdown}
            class="form-control"
          />
        </div>
      </form>
      <a href="/">
        <button on:click={submitPost} class="btn btn-primary mt-4">
          Save
        </button>
      </a>
      <a href="/" class="btn btn-secondary mt-4">Cancel</a>
    </div>
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</main>
