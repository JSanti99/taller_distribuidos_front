<script lang="ts">
  export let id: string;
  export let value: string;
  export let placeholder: string;
</script>

<input
  {id}
  type="text"
  {placeholder}
  bind:value
  class:border-red-400={!value.length}
  class="px-4 py-2 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-gray-200 text-gray-600"
/>

<style>
</style>
