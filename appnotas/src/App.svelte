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
    width: 1000px;
    margin: 0 auto;
    justify-content: center;
    flex-flow: row wrap;
    text-align: left;
  }

  .titulo {
    width: 800px;
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
	
	.azul {
		background:#6697c8;
		color: #fff;
		
	}

	.cajaroja {
		background:#ff0b0b;
		color: #fff;
	}

	.cajanaranja {
		background:#ff9900;
		color: #fff;
	}

	.cajaverde {
		background:#2cdd78;
		color: #fff;
	}

	.gris {
		background: #f0f0f0;
		color: #a39d9d;
	}

	.blanco {
		background: #feffe3;
		color: #a39d9d;
	}

  .grid-container {
    display: grid;
    width: 800px;
    grid-template-rows: 200px 250px 200px;
    grid-template-columns: 1fr 3fr 6fr;

    grid-gap: 15px;
  }

  .grid-1 {
    text-align: center;
    grid-row: 1 / 1;
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
    grid-template-columns: 2fr 1fr;
    grid-gap: 5px;
    padding: 10px 30px;
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
    padding: 10px;
  }

  .grid-3 {
    text-align: center;
    border: #f0f0f0 1px;
		grid-column: 1/3;
		grid-row: 2/ 2;
    grid-gap: 0px;
    padding: 20px 0px;
	}

	.grid-4 {
		border: #f0f0f0 1px solid;
		background: #feffe3;
		grid-row: 3/ 1;
		grid-column: 3/3;
		grid-gap: 20px;
		padding: 10px;
	}

	.grid-5 {
		border: #f0f0f0 1px;
		grid-column: 3/3;
		padding: 0px 20px;
	}
	
.notas {
	 width: 100%;
	 border: 1px solid #6697c8; 
	 	border-collapse: collapse;
	
}

.notas thead th {
	background: #6697c8;
	color: #f0f0f0;
	border: 1px solid #6697c8; 
	border-collapse: collapse;
	padding: 10px;
	font-weight: normal;
	
}

.notas tbody td {
	 width: 25%;
		text-align: center;
		border: 1px solid #6697c8;
		border-collapse: collapse;
}

.notas .mat {
	text-align: left;
	padding-left: 10px;
}

.notas tfoot th {
	background: #6697c8;
	color: #f0f0f0;
	text-align: right;
	padding: 10px;
	font-weight: normal;
}

.notas tfoot td {
	border: 1px solid #6697c8;
	font-weight: bold;
}

.notas tbody td button {
	border: none;
	background: none;
	
}

li, ul {
	list-style-type: none;
	margin-top: 0px;
	margin-bottom: 0px;
	
}

.colores  {
	width: 100%;
	border: none;
	border-collapse: collapse;
	
}

.colores td {
	text-align: center;
	margin: 10px;
	padding: 10px;
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
        <table class="notas">
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
              <th>Promedio</th>
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

			<div class="grid-4">
				<li>- Al hacer click en el botón <strong>agregar</strong> se adiciona la nota a la tabla y recalcula el promedio de todas las notas.</li>
				<li>- Al hacer click en el icono rojo al final de cada fila de la tabla debe eliminar la nota y recalcular el promedio</li>
				<li>- Color de las notas y el prmedio:</li>
				<ul><li>- Entre 0 y 2.5 = rojo</li>
				<li>- Entre 2.6 y 2.9 = naranja</li>
				<li>- Entre 3.0 y 5.0 = verde</li></ul>
				<li>-Al agregar una nueva materia no debe permitir:</li>
				<ul><li>- Agregar materias vacias</li>
				<li>- Notas no numéricas</li>
				<li>- Notas por fuera de 0 y 5.0</li></ul>
				<li>- Se debe resperar los colores, alineación, fuentes, etc</li>
				<li>- El título de la página debe tener el nombre del estudiante y su docimento de identidad.</li>
				<li>- Esta nota debe presentarse en la pagina</li>
				<li>- La entrega consiste en la URL del sitio publicado en Netlify</li>
			</div>

			<div class="grid-5">
				<table class="colores">
					<tr>
						<td class="azul">#6697c8</td>
						<td class="cajaroja">#FF0B0B</td>
						<td class="gris">#F0F0F0</td>
					</tr>
					<tr>
						<td class="cajanaranja">#FF9900</td>
						<td class="cajaverde">#2CDD78</td>
						<td class="blanco">#FEFFF3</td>
					</tr>
				</table>
			</div>
    </div>

  </div>
</div>
