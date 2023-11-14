<script>
  import { onMount } from 'svelte';
  let contributions = [];

  onMount(async () => {
    const res = await fetch('/api/contributions'); // replace with your API endpoint
    contributions = await res.json();
  });

  function getContributionColor(level) {
    switch (level) {
      case 0: return '#ebedf0'; // no contributions
      case 1: return '#9be9a8'; // 1-2 contributions
      case 2: return '#40c463'; // 3-4 contributions
      case 3: return '#30a14e'; // 5-6 contributions
      case 4: return '#216e39'; // 7+ contributions
      default: return '#ebedf0';
    }
  }
</script>

<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }

  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: center;
  }

  tr:nth-child(even) {
    background-color: #f2f2f2;
  }

  th {
    background-color: #4CAF50;
    color: white;
  }

  .contribution {
    display: inline-block;
    width: 10px;
    height: 10px;
  }
</style>

<table>
  <thead>
    <tr>
      <th>Month</th>
      <th>Day</th>
      <th>Contributions</th>
    </tr>
  </thead>
  <tbody>
    {#each contributions as { month, day, level }}
      <tr>
        <td>{month}</td>
        <td>{day}</td>
        <td>
          <div class="contribution" style="background-color: {getContributionColor(level)};"></div>
        </td>
      </tr>
    {/each}
  </tbody>
</table>
