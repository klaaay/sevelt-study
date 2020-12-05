<script>
  import Product from "./Product.svelte";
  import Modal from "./Modal.svelte";

  const products = [
    {
      id: "p1",
      tilte: "A book",
      price: 9.99,
    },
    {
      id: "p2",
      tilte: "A book",
      price: 10.99,
      bestseller: true,
    },
  ];

  function addToCart(event) {
    console.log(event);
  }

  function deleteProduct(event) {
    console.log(event.detail);
  }

  let showModal = false;
</script>

{#each products as product}
  <Product {...product} on:add-to-cart={addToCart} on:delete={deleteProduct} />
{/each}

<button on:click={() => (showModal = true)}>Show Modal</button>
{#if showModal}
  <Modal
    on:cancle={() => (showModal = false)}
    on:close={() => (showModal = false)}
    showModal>
    <h1 slot="header">HI</h1>
    <p>This works really</p>
  </Modal>
{/if}
