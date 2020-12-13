<script>
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
  <h1>{data.posts[0].title}</h1>
  <article>
    {@html data.posts[0].html}
  </article>
{:catch error}
  <p style="color: red">{error.message}</p>
{/await}
