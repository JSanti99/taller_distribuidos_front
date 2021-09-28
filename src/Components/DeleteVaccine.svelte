<script lang="ts">
  export let row;
  export let actualizar: Function;

  const handleDelete = () => {
    fetch(`http://localhost:3000/vaccine/${row._id}`, {
      method: "DELETE",
    })
      .then(async (res) => {
        const data = await res.json();
        actualizar(row._id);
        console.log(data);
      })
      .catch((err) => {
        console.log(err);
      });
  };
</script>

<button
  class="h-8 flex justify-center items-center text-white bg-red-600 rounded-full hover:bg-red-700 active:shadow-lg mouse shadow transition ease-in duration-200 focus:outline-none"
  on:click={handleDelete}
>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    class="h-6 w-6"
    fill="none"
    viewBox="0 0 24 24"
    stroke="currentColor"
  >
    <path
      stroke-linecap="round"
      stroke-linejoin="round"
      stroke-width="2"
      d="M5 13l4 4L19 7"
    />
  </svg>
  <span>DEL</span>
</button>
