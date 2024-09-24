<script>
    const data = {
    labels: ['Income', 'Expenses'],
    datasets: [
        {
        data: [3400,2500],
        backgroundColor: [
            'rgba(113, 205, 205,0.4)',
            'rgba(255, 134,159,0.4)',
            
        ],
        borderWidth: 2,
        borderColor: [
            'rgba(113, 205, 205, 1)',
            'rgba(255, 134, 159, 1)',
            
        ],
        },
    ],
    };

    import { Bar } from 'svelte-chartjs';
  
    import {
      Chart,
      Title,
      Tooltip,
      Legend,
      BarElement,
      CategoryScale,
      LinearScale,
    } from 'chart.js';
  
    Chart.register(
      Title,
      Tooltip,
      Legend,
      BarElement,
      CategoryScale,
      LinearScale
    );
  </script>
  
  <Bar {data} options={{ responsive: true, plugins:{legend:{display: false}}}} />
  

