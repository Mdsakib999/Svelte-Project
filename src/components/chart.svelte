<!-- src/routes/PieChart.svelte -->
<script>
    import { onMount, afterUpdate } from 'svelte';
    import Chart from 'chart.js/auto';
  
    let countries = [];
    let populationData = [];
    let chart;
  
    onMount(async () => {
      try {
        const response = await fetch('https://restcountries.com/v3.1/all');
        if (response.ok) {
          countries = await response.json();
          populationData = countries.slice(0, 12).map(country => ({
            label: country.name.common,
            data: country.population,
          }));
          createPieChart();
        } else {
          console.error('Failed to fetch data');
        }
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    });
  
    afterUpdate(() => {
      if (chart) {
        chart.destroy(); 
        createPieChart();
      }
    });
  
    
  
    function createPieChart() {
      const canvas = document.getElementById('populationChart');
      if (canvas) {
        const ctx = canvas.getContext('2d');
        chart = new Chart(ctx, {
          type: 'doughnut',
          data: {
            labels: populationData.map(data => data.label),
            datasets: [{
              data: populationData.map(data => data.data),
              backgroundColor: [
                'rgba(255, 99, 132, 0.5)',
                'rgba(255, 159, 64, 0.5)',
                'rgba(255, 205, 86, 0.5)',
                'rgba(75, 192, 192, 0.5)',
                'rgba(54, 162, 235, 0.5)',
                'rgba(153, 102, 255, 0.5)',
                'rgba(201, 203, 207, 0.5)',
                'rgba(255, 99, 132, 0.5)',
                'rgba(255, 159, 64, 0.5)',
                'rgba(255, 205, 86, 0.5)',
                'rgba(75, 192, 192, 0.5)',
                'rgba(54, 162, 235, 0.5)',
              ],
            }],
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
          },
        });
      }
    }
  </script>

  <h1 class="mt-4 mb-6 text-center text-3xl font-bold">This chart</h1>

  <canvas id="populationChart" width="400" height="400"></canvas>
  