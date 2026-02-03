<script>
  export let label = "Click me";
  export let bgColor = "bg-blue-500";
  export let onClick = () => {};
</script>

<button
  class={`px-6 py-3 rounded-xl text-white font-semibold shadow-md transition 
  ${bgColor} 
  hover:opacity-90 
  focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-black
  active:scale-95`}
    on:click={onClick}
>
    {label}
</button>
