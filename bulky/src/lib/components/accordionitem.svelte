<script lang="ts">
    let { title, children, isOpen = $bindable(false) }  = $props();

    function toggle() {
        isOpen = !isOpen;
    }
</script>

<div class="accordion-item">
  <button onclick={toggle} class="accordion-header bg-gray-200 p-4 w-full text-left flex justify-between items-center">
    <span>{title}</span>
    <span>{isOpen ? '-' : '+'}</span>
  </button>
  
  {#if isOpen}
    <div class="accordion-content">
      {@render children()}
    </div>
  {/if}
</div>
