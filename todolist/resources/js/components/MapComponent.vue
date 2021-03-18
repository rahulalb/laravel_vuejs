<script>
import  countryData from '../countries.json'

import { generateChart } from 'vue-chartjs'
import {choropleth, topojson} from  'chartjs-chart-geo'

const countries = topojson.feature(countryData, countryData.objects.countries).features

const ChoroplethChart = generateChart("choropleth", "choropleth");

export default {
  extends: ChoroplethChart,
  mounted () {
        this.renderChart({
        labels: countries.map((d) => d.properties.name),
        datasets: [
            {
                label: 'Countries',
                backgroundColor: context => {
                  if (context.dataIndex == null) {
                    return null;
                  }
                  const value = context.dataset.data[context.dataIndex];
                  return `rgb(0, 0, ${value.value * 255})`;
                },
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
