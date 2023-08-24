<script>
  let url = window.location.href;
  url = url.split("/");
  let id = url[5];
  let post;
  async function fetchData() {
    let link = "http://localhost:3000/post/show/";
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
      <h1 class="mb-1">Title: {post.title}</h1>
      <div id="createdAt">{post.createdAt.substring(0, 10)}</div>
      <a href="/" class="btn btn-secondary"> All Articles</a>
      <a href="/#/edit/{id}" class="btn btn-info"> Edit</a>
      <!-- <div>
      <img src="{post.image}" alt="A Pic">
      {console.log(post.image)}
    </div> -->
    <div style = "width:800px; margin:0 auto; margin-right:20px">
      <img src="/assets/babar.jpg" width="550" height="300" alt="" />
    </div>
      <div id="markdownShow">
        {post.markdown}
      </div>
    </div>
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</main>
