<script>
  import { createEventDispatcher } from "svelte";
  let dispatch = createEventDispatcher();

  export let endpoint;

  async function getData() {
    const res = await fetch(endpoint);
    const data = await res.json();
    console.log(data);
    if (res.ok) {
      return data;
    } else {
      throw new Error(data);
    }
  }
  let promise = getData();
</script>

{#await promise}
  <p>...waiting</p>
{:then data}
  <ul>
    {#each data.posts as post}
      <li>
        <a
          on:click|preventDefault={() => dispatch('getpost', post.id)}
          href={post.slug}>{post.title}</a>
      </li>
    {/each}
  </ul>
{:catch error}
  <p style="color: red">{error.message}</p>
{/await}
