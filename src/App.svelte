<script>
  import { tick } from "svelte";
  import Product from "./Product.svelte";
  import Modal from "./Modal.svelte";

  const products = [
    {
      id: "p1",
      tilte: "A book",
      price: 9.99,
    },
  ];

  let closeable = false;

  function addToCart(event) {
    console.log(event);
  }

  function deleteProduct(event) {
    console.log(event.detail);
  }

  let showModal = false;

  let text = "this is some dummy text!";

  function transform(event) {
    if (event.which !== 9) {
      return;
    }
    event.preventDefault();
    const selectionStart = event.target.selectionStart;
    const selectionEnd = event.target.selectionEnd;
    const value = event.target.value;
    text =
      value.slice(0, selectionStart) +
      value.slice(selectionStart, selectionEnd).toUpperCase() +
      value.slice(selectionEnd);

    tick().then(() => {
      event.target.selectionStart = selectionStart;
      event.target.selectionEnd = selectionEnd;
    });
  }
</script>

{#each products as product}
  <Product {...product} on:add-to-cart={addToCart} on:delete={deleteProduct} />
{/each}

<button on:click={() => (showModal = true)}>Show Modal</button>
{#if showModal}
  <Modal
    on:cancle={() => (showModal = false)}
    on:close={() => (showModal = false)}
    let:didAgree={closeable}
    showModal>
    <h1 slot="header">HI</h1>
    <p>This works really</p>
    <button
      slot="footer"
      on:click={() => (showModal = false)}
      disabled={!closeable}>Cancel</button>
  </Modal>
{/if}

<textarea rows="3" on:keydown={transform} value={text} />
