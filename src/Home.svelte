<script>
  let data = null;
  async function fetchData() {
    try {
      const response = await fetch("http://localhost:3000/post");
      if (!response.ok) {
        throw new Error("Network response was not ok");
      }
      data = await response.json();
      return data.itemData;
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  }
  export function removeItem(id) {
    let link = "http://localhost:3000/post/";
    let result = link.concat(id);
    fetch(result, {
      method: "DELETE",
    })
      .then((response) => response.json())
      .then((res) => console.log(res));
    location.reload();
  }
</script>

<main>
  <!-- Just an image -->
  <nav class="navbar navbar-light bg-light">
    <a class="navbar-brand" href="/">
      <img src="/assets/112121.jpg" width="30" height="30" alt="" />
      Sports Blog
    </a>
    
  </nav>
  <div class="container">
    <h1 class="mb-4 mt-3">Blog Articles</h1>
    <a href="#/new" class="btn btn-success">New Article</a>
    {#await fetchData()}
      <p>Data to be displayed</p>
    {:then data}
      {#each data as post}
        <div class="card mt-4">
          <div class="card-body">
            <h2 class="card-title"><b>{post.title}</b></h2>

            <div class="text">
              Created on: {post.createdAt.substring(0, 10)}
            </div>
            <div class="card-text-mb-2">
              {post.description}
            </div>

            <a href="#/show/{post._id}" class="btn btn-primary">Read More</a>
            <a href="#/edit/{post._id}" class="btn btn-info">Edit</a>
            <button on:click={() => removeItem(post._id)} class="btn btn-danger"
              >Delete</button
            >
          </div>
        </div>
      {/each}
    {:catch error}
      <p style="color: red">{error.message}</p>
    {/await}
  </div>
</main>



