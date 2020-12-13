<script>
  let nombre = "Daniel Carvajal Hernández";
  let documento = "1020761293";
  let promedio = 0;

  let notas = [];

  let nota = {
    materia: "",
    nota: 0
  };

  const agregar = e => {
    e.preventDefault();
    console.log(nota);

    notas = notas.concat(nota);
    console.log(nota);
    const sumatoriaObjeto = notas.reduce(
      (a, next) => {
        return { nota: a.nota + next.nota };
      },
      { nota: 0 }
    );

    promedio = sumatoriaObjeto.nota / notas.length;
    borrar();
  };

  const borrar = () => {
    nota = {
      materia: "",
      nota: 0
    };
  };

  const eliminar = materia => {
    console.log(materia);
    notas = notas.filter(nota => nota.materia !== materia);
    const sumatoriaObjeto = notas.reduce(
      (a, next) => {
        return { nota: a.nota + next.nota };
      },
      { nota: 0 }
    );

    promedio = sumatoriaObjeto.nota / notas.length;
  };
</script>

<style>
  .contenedor {
    display: flex;
    height: 100px;
    width: 600px;
    margin: 0 auto;
    justify-content: center;
    flex-flow: row wrap;
    text-align: left;
  }

  .titulo {
    width: 600px;
  }

  img {
    width: 60px;
  }

  .rojo {
    color: #ff0b0b;
  }

  .naranja {
    color: #ff9900;
  }

  .verde {
    color: #2cd078;
  }

  .grid-container {
    display: grid;
    width: 600px;
    grid-template-rows: 250px 250px;
    grid-template-columns: 1fr 7fr;

    grid-gap: 1px;
  }

  .grid-1 {
    text-align: center;
    grid-row: 1 / 2;
    grid-gap: 5px;
  }

  .grid-2 {
    background: #f0f0f0;
    text-align: letf;
    border: blue 1px solid;
    align-self: center;
    grid-gap: 0px;
  }

  form {
    display: grid;
    grid-template-columns: 1fr 2fr;
    grid-gap: 5px;
    padding: 20px 40px;
  }

  form button {
    grid-column: 2/3;
    background: #a39d9d;
    color: #f0f0f0;
  }

  .cabecera {
    background: #6697c8;
    color: #feffe3;
    text-align: left;
    padding: 20px;
  }

  .grid-3 {
    text-align: center;
    border: #f0f0f0 1px solid;
    grid-column: 1/3;
    grid-gap: 20px;
    padding: 20px;
	}
	
	table {
	 width: 100%;
	 border: 1px solid #6697c8; 
	 	border-collapse: collapse;
	
}

table thead th {
	background: #6697c8;
	color: #f0f0f0;
	border: 1px solid #6697c8; 
	border-collapse: collapse;
	padding: 10px;
	font-weight: normal;
	
}
table tbody td {
	 width: 25%;
		text-align: center;
		border: 1px solid #6697c8;
		
		border-collapse: collapse;
}

.mat {
	text-align: left;
	padding-left: 10px;
}

table tfoot th {
	background: #6697c8;
	color: #f0f0f0;
	text-align: right;
	padding: 10px;
	font-weight: normal;
}

table tfoot td {
	border: 1px solid #6697c8;
	font-weight: bold;
}

table tbody td button {
	border: none;
	background: none;
	
}

</style>

<div class="contenedor">

  <div class="titulo">
    Notas de {nombre} - CC: {documento}
    <hr />
  </div>

  <div class="titulo">
    <div class="grid-container">

      <div class="grid-1">
        <img src="Daniel.jpeg" alt="" />
      </div>

      <div class="grid-2">

        <div class="cabecera">Nueva nota</div>
        <form action="" on:submit={agregar}>

          <label for="materia">Materia</label>
          <input
            type="text"
            name="materia"
            id="materia"
            bind:value={nota.materia}
            required />
          <label for="notas">Nota</label>
          <input
            type="number"
            step="any"
            name="notas"
            id="notas"
            bind:value={nota.nota}
            required
            min="0"
            max="5" />
          <button>Agregar</button>
        </form>
      </div>

      <div class="grid-3">
        <table>
          <thead>
            <tr>

              <th scope="col">Materia</th>
              <th scope="col">Nota</th>
              <th scope="col">icono</th>
            </tr>
          </thead>
          <tbody>
            {#each notas as dato}
              <tr>

                <td class="mat">{dato.materia}</td>

                {#if dato.nota <= 2.5}
                  <td class="rojo">{dato.nota}</td>
                {:else if dato.nota <= 2.9}
                  <td class="naranja">{dato.nota}</td>
                {:else}
                  <td class="verde">{dato.nota}</td>
                {/if}

                <td>
                  <button on:click={eliminar(dato.materia)}>
                    <i class="fas fa-trash-alt rojo" />
                  </button>
                </td>
              </tr>
            {/each}

          </tbody>
          <tfoot>
            <tr>
              <th>promedio</th>
              {#if promedio <= 2.5}
                <td class="rojo">{promedio}</td>
              {:else if promedio <= 2.9}
                <td class="naranja">{promedio}</td>
              {:else}
                <td class="verde">{promedio}</td>
              {/if}

            </tr>
          </tfoot>
        </table>

      </div>
    </div>

  </div>
</div>
