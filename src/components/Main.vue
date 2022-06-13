<template>
  <div class = "container">
    <div class = "card">
      <h3>Total de entradas de viajeros interinsulares: 2011 - Q12022</h3>
      <LineChart :labels = "labelsBigChart" :dataSet = "datasetsBigChart"/>
    </div>
    <div class = "card">
      <LineChart :labels = "labelsTotalPorIslas" :dataSet = "datasetsTotalPorIslas"/>
    </div>

    <div class = "double-row">
      <div class = "card">
        <h2>2021 - 2020</h2>
        <h4>Gran canaria recibió un</h4>
        <h1> 77,54% </h1>
        <h4> más de visitantes en 2021 que en 2020</h4>
      </div>
      <div class = "card">
        <h2>2022</h2>
        <h4>La isla con mayor número de visitantes en 2022 fue</h4>
        <h3> Gran Canaria </h3>
        <h1>367407</h1>
        <h4>visitantes</h4>
      </div>
    </div>
  </div>
</template>

<script>
import LineChart from './LineChart.vue'
import * as d3 from "d3"

export default {
  name: 'Main',
  components: {
    LineChart
  },
  props: {
    
  },
  data () {
    return {
      totalesInterinsular: [],
      totalPorIslas: []
    }
  },
  computed: {
    labelsTotalPorIslas () {
      return this.totalPorIslas.filter(row => row['Isla de alojamiento'] == 'Lanzarote').map(row => parseInt(row.Periodo))
    },
    datasetsTotalPorIslas () {
      return [{
        label: 'Lanzarote',
        data: this.totalPorIslas.filter(row => row['Isla de alojamiento'] == 'Lanzarote').map(row => parseInt(row.Valor)),
        borderColor: '#01295f',
        pointBackgroundColor: '#01295f'
      },
      {
        label: 'Gran Canaria',
        data: this.totalPorIslas.filter(row => row['Isla de alojamiento'] == 'Gran Canaria').map(row => parseInt(row.Valor)),
        borderColor: '#452493',
        pointBackgroundColor: '#452493'
      },
      {
        label: 'Tenerife',
        data: this.totalPorIslas.filter(row => row['Isla de alojamiento'] == 'Tenerife').map(row => parseInt(row.Valor)),
        borderColor: '#fd151b',
        pointBackgroundColor: '#fd151b'
      },
      {
        label: 'Fuerteventura',
        data: this.totalPorIslas.filter(row => row['Isla de alojamiento'] == 'Fuerteventura').map(row => parseInt(row.Valor)),
        borderColor: '#ffb30f',
        pointBackgroundColor: '#ffb30f',
      },
      {
        label: 'La Palma',
        data: this.totalPorIslas.filter(row => row['Isla de alojamiento'] == 'La Palma').map(row => parseInt(row.Valor)),
        borderColor: '#52b69a',
        pointBackgroundColor: '#52b69a',
      },
      {
        label: 'El Hierro',
        data: this.totalPorIslas.filter(row => row['Isla de alojamiento'] == 'El Hierro').map(row => parseInt(row.Valor)),
        borderColor: '#34a0a4',
        pointBackgroundColor: '#34a0a4',

      },
      {
        label: 'La Gomera',
        data: this.totalPorIslas.filter(row => row['Isla de alojamiento'] == 'La Gomeras').map(row => parseInt(row.Valor)),
        borderColor: '#ff0fb7',
        pointBackgroundColor: '#ff0fb7',

      }
      ]
    },
    datasetsBigChart () {
      return [{
        label: 'Número total de pasajeros llegados a Canarias entre 2011 y febrero de 2022',
        data: this.totalesInterinsular.map(row => parseInt(row.Valor)),
        borderColor: '#fd151b',
        pointBackgroundColor: '#fd151b'
      }]
    },
    labelsBigChart () {
      return this.totalesInterinsular.map(row => row.Periodo)
    } 
  },
  async created()  {
    this.totalesInterinsular = await d3.csv('data/totalesInterinsular.csv')
    this.totalPorIslas = await d3.csv('data/totalPorIslas.csv')
  },
}
</script>

<style>

.container {
}

.card {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  text-align: left; 
  padding: 2rem 2rem; 
  background-color: white;
  border-radius: 1rem;
  margin-bottom: 3rem;
  flex-grow: 2;
  box-shadow: 5px -1px 36px -3px rgba(0,0,0,0.27);
}

.double-row {
  display: flex;
  flex-direction: row;
  width: 100%;
  gap: 4rem;
}

h1 {
  margin: 1px;
  font-size: 4rem;
}

h2 {
  margin: 0;
  color: #b6ccfe;
}

h3 {
  margin: 2px;
  color: #abc4ff;
}

h4 {
  margin: 5px 0;
  color: #d7e3fc;
}

</style>