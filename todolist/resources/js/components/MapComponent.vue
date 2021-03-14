<script>
import * as countryData from '../countries.json'

import { generateChart } from 'vue-chartjs'
import ChartGeo from  'chartjs-chart-geo'
const countries = ChartGeo.topojson.feature(countryData, countryData.objects.countries).features

const ChoroplethMap = generateChart('choropleth-map', 'choropleth')

export default {
  extends: ChoroplethMap,
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
