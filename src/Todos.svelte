<script>
  import TodoItem from './TodoItem.svelte'

  let nuevaTareaTitulo = ''
  let filtroActual = 'filtro-todos'
  let siguienteId = 4

  let tareasData = [
    {
      id: 1,
      titulo: 'Mi primera tarea',
      completada: false,
    },
    {
      id: 2,
      titulo: 'Mi segunda tarea',
      completada: false,
    },
    {
      id: 3,
      titulo: 'Mi tercera tarea',
      completada: false,
    },
  ]

  /* Functiones: */
  function agregarTarea(event) {
    console.log(event)
    if (nuevaTareaTitulo === '') return

    if (event.key === 'Enter' || event.type === 'submit') {
      tareasData = [
        ...tareasData,
        {
          id: siguienteId,
          completada: false,
          titulo: nuevaTareaTitulo,
        },
      ]

      siguienteId += 1
      nuevaTareaTitulo = ''
    }
  }

  function checkTareas(event) {
    tareasData.forEach((tarea) => (tarea.completada = event.target.checked))
    tareasData = tareasData
  }

  function actualizarFiltro(nuevoFiltro) {
    console.info('Nuevo filtro: ' + nuevoFiltro)
    filtroActual = nuevoFiltro
  }

  function borrarCompletados() {
    // Esta función se encarga de quitar las tareas con el status de completada del array 'tareasData'
    tareasData = tareasData.filter((tarea) => !tarea.completada)
  }

  $: tareasPendientes = tareasDataFiltradas.filter((tarea) => !tarea.completada).length
  $: tareasDataFiltradas =
    filtroActual === 'filtro-todos'
      ? tareasData
      : filtroActual === 'filtro-completadas'
      ? tareasData.filter((tarea) => tarea.completada)
      : tareasData.filter((tarea) => !tarea.completada)

  /* Manejadores: */
  function manejarBorrarTarea(event) {
    tareasData = tareasData.filter((tarea) => tarea.id !== event.detail.id)
  }

  function manejarCompletada(event) {
    const tareaIndex = tareasData.findIndex((tarea) => tarea.id === event.detail.id)
    const tareaActualizada = {
      ...tareasData[tareaIndex],
      completada: !tareasData[tareaIndex].completada,
    }
    tareasData = [...tareasData.slice(0, tareaIndex), tareaActualizada, ...tareasData.slice(tareaIndex + 1)]
  }
</script>

<div class="contenedor">
  <a href="#"><img src={'/imgs/todo.jpeg'} class="logo" alt="todo" /></a>

  <h2>Aplicación de Tareas</h2>

  <form on:submit|preventDefault={agregarTarea} on:keydown={agregarTarea}>
    <input type="text" class="tarea-input" placeholder="Agregar tarea..." name="titulo" id="titulo" bind:value={nuevaTareaTitulo} />
    <button type="submit">Send</button>
  </form>

  {#each tareasDataFiltradas as tarea}
    <div class="tarea-item">
      <TodoItem {...tarea} on:borrarTarea={manejarBorrarTarea} on:toggleCompletada={manejarCompletada} />
    </div>
  {/each}

  <div class="contenedorDatos">
    <div>
      <label><input class="input" type="checkbox" on:change={checkTareas} />Seleccionar todo</label>
    </div>
    {#if tareasPendientes === 0}
      <div>No quedan tareas pendientes.</div>
    {:else if tareasPendientes === 1}
      <div>queda {tareasPendientes} tarea pendiente.</div>
    {:else}
      <div>quedan {tareasPendientes} tareas pendientes.</div>
    {/if}
  </div>
  <div class="contenedorDatos">
    <div>
      <button on:click={() => actualizarFiltro('filtro-todos')} class:activa={filtroActual === 'filtro-todos'}>Todos</button>
      <button on:click={() => actualizarFiltro('filtro-pendientes')} class:activa={filtroActual === 'filtro-pendientes'}>Pendientes</button>
      <button on:click={() => actualizarFiltro('filtro-completadas')} class:activa={filtroActual === 'filtro-completadas'}
        >Completados</button
      >
    </div>
    <div>
      <button class="boton-icono" on:click={borrarCompletados}>
        <img class="icono" src={'/imgs/icons8-delete.svg'} alt="erase" />
        <span>Borrar completados</span>
      </button>
    </div>
  </div>
</div>

<style>
  .contenedor {
    max-width: 800px;
    margin: 10px auto;
  }
  .logo {
    display: block;
    margin: 20px auto;
    width: 150px;
    height: auto;
  }
  .boton-icono {
    display: flex;
    flex-direction: row;
    justify-items: center;
    align-items: center;
    padding: 5px 10px;
  }
  .icono {
    width: 30px;
    height: 30px;
    margin: 4px;
  }
  form {
    display: grid;
    grid-template-columns: 3fr 1fr;
    margin-bottom: 20px;
    gap: 5px;
  }
  @media (max-width: 400px) {
    form {
      display: grid;
      grid-template-columns: 1fr;
      grid-template-rows: 1fr 1fr;
    }
  }
  .tarea-input {
    width: 100%;
    padding: 10px 20px;
    font-size: 18px;
  }
  .contenedorDatos {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid orange;
    padding-top: 10px;
    margin-bottom: 12px;
  }

  .input {
    margin-right: 12px;
  }
  button {
    background-color: orangered;
    color: white;
    appearance: none;
    border: none;
    padding: 5px;
    height: 100%;
  }
  button:hover {
    background-color: orange;
  }
  button:focus {
    outline: none;
  }
  .activa {
    background-color: lightsalmon;
  }
</style>
