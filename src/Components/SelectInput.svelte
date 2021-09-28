<script>
  import Select from "svelte-select";

  // const items = [
  // 	{value: 'chocolate', label: '🍫 Chocolate', group: 'Sweet'},
  // {value: 'pizza', label: '🍕 Pizza', group: 'Savory'},
  // {value: 'cake', label: '🎂 Cake', group: 'Sweet'},
  // {value: 'cookies', label: '🍪 Cookies', group: 'Savory'},
  // {value: 'ice-cream', label: '🍦 Ice Cream', group: 'Sweet'}
  // ];
  export let items;
  export let id;
  export let handleSelect;
  export let handleClear;
</script>

<Select {id} {items} on:select={handleSelect} on:clear={handleClear} />
