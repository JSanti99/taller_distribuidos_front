<script lang="ts">
  export let text: string;
</script>

<fieldset class="border border-solid border-gray-300 p-3 m-0 w-auto">
  <legend class="text-gray-500 font-bold text-left px-2">{text}</legend>
  <slot />
</fieldset>

<style>
</style>
