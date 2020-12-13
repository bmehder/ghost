<script>
  import Posts from "./Posts.svelte";
  import Post from "./Post.svelte";

  let isSingle = false;
  let postEndpoint;

  const getPost = (e) => {
    postEndpoint = `http://localhost:2368/ghost/api/v3/content/posts/${e.detail}?key=3a0d5f42eef6297bed693c32ff`;
    isSingle = true;
  };

  // $: console.log(postEndpoint);
</script>

{#if isSingle}
  {#if postEndpoint !== undefined}
    <button on:click={() => (isSingle = false)}>&laquo; Back</button>
    <Post endpoint={postEndpoint} />
  {/if}
{:else}
  <Posts
    on:getpost={getPost}
    endpoint="http://localhost:2368/ghost/api/v3/content/posts/?key=3a0d5f42eef6297bed693c32ff" />
{/if}
