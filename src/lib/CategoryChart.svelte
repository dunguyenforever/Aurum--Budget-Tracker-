<script>
    const data = {
    labels: [
      "Rent",
      "Groceries",
      "Utilities",
      "Transportation",
      "Entertainment",
      "Healthcare",
      "Dining Out"
    ],
    datasets: [
        {
        data: [300, 50, 100, 40, 120],
        backgroundColor: [
            '#63013e',
            '#d4af37',
            '#108090',
            '#e6e6fa',
            '#0d0d0d',
            '#f5f5f5',
        ],
        hoverBackgroundColor: [
            '#63013e',
            '#d4af37',
            '#108090',
            '#e6e6fa',
            '#0d0d0d',
            '#f5f5f5',
        ],
        },
    ],
    };
    import { Pie } from 'svelte-chartjs';
    import {
      Chart as ChartJS,
      Title,
      Tooltip,
      Legend,
      ArcElement,
      CategoryScale,
    } from 'chart.js';
  
    ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale);
  </script>
  
<Pie {data} options={{ responsive: true, aspectRatio: 2 }} />