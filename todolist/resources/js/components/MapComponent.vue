<script>
import  countryData from '../countries.json'

import { generateChart } from 'vue-chartjs'
import {Choropleth, topojson} from  'chartjs-chart-geo'
const countries = topojson.feature(countryData, countryData.objects.countries).features


const ChoroplethChart = generateChart('choropleth-map', "choropleth")


export default {
  extends: ChoroplethChart,
  mounted () {
        this.renderChart({
        labels: countries.map((d) => d.properties.name),
        datasets: [
            {
                label: 'Countries',
                data: countries.map((d) => ({feature: d, value: Math.random()}))
            }
        ]
    }, {
      showOutline: true,
      showGraticule: true,
      plugins: {
        legend: {
          display: false
        },
      },
      scales: {
        xy: {
          projection: 'equalEarth'
        }
      }
    })
    }
}

</script>
