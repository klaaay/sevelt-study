<script>
  import Product from "./Product.svelte";

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
</script>

{#each products as product}
  <Product {...product} on:add-to-cart={addToCart} on:delete={deleteProduct} />
{/each}
