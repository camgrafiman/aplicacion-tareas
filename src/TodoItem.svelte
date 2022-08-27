<script>
  import { createEventDispatcher } from 'svelte'
  import { fly } from 'svelte/transition'

  const dispatch = createEventDispatcher()

  /* props y funciones del componente: */

  export let id
  export let titulo
  export let completada

  function borrarTarea() {
    dispatch('borrarTarea', {
      id: id,
    })
  }
  function toggleCompletada() {
    dispatch('toggleCompletada', {
      id: id,
    })
  }
</script>

<div class="tarea-item">
  <div class="tarea-item-izq" transition:fly={{ y: 20, duration: 300 }}>
    <input type="checkbox" bind:checked={completada} on:change={toggleCompletada} />
    <div class="tarea-item-label" class:completada>{titulo}</div>
  </div>
  <div class="tarea-eliminar" on:click={borrarTarea}>
    <img src={'imgs/icons8-close.svg'} alt="" />
  </div>
</div>

<style>
  .tarea-item {
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    animation-duration: 0.4s;
  }
  .tarea-eliminar {
    cursor: pointer;
    margin-left: 14px;
    border: none;
    width: 30px;
    height: 30px;
  }
  .tarea-eliminar > img {
    width: inherit;
    height: inherit;
  }
  .tarea-eliminar:hover {
    transform: scale(1.1);
  }
  .tarea-item-izq {
    display: flex;
    align-items: center;
  }
  .tarea-item-label {
    border: 1px solid white;
    margin-left: 12px;
  }
  .completada {
    text-decoration: line-through;
    color: lightsalmon;
    font-style: italic;
  }
</style>
