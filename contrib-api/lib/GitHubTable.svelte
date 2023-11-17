<script>
  export let contributions = [];
  // 53 week array with additional 7 day array.
  let weeks = Array.from({ length: 53 }, () => Array(7).fill(null));

  // Populates the weeks
  contributions.forEach((contribution, index) => {
    const weekIndex = Math.floor(index / 7);
    const dayIndex = index % 7;
    weeks[weekIndex][dayIndex] = contribution;
  });

  // Calculate the total contributions
  $: totalContributions = contributions.reduce((total, contribution) => {
    return total + (contribution?.count || 0);
  }, 0);
  

</script>

<style>
  :global(body) {
    background-color: #0a0908;
    margin: 0;
    padding: 0;
  }
  
  .github-contributions {
    color: #c9d1d9;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
    font-size: 12px;
    background-color: #0a0908;
    padding: 16px;
    margin: auto;
    width: fit-content;
    position: relative;
  }

  .contributions-header {
  position: absolute;
  top: -20px; 
  left: 0; 
  font-size: 12px;
  font-weight: 600;
}

  .contributions-container {
    border: 0.5px solid #fff;
    padding: 8px;
    display: flex;
    gap: 4px;
    align-items: flex-start;
    padding-left: 20px; 
    background-color: #0d1117;
  }

  .week-container {
  display: grid;
  grid-template-rows: repeat(7, 1fr);
  border: none;
  border-radius: 0; 
  overflow: hidden;
}

  .contribution-cell {
  color: #8b949e;
  width: 10px;
  height: 10px; 
  border-radius: 2px;
  background-color: #161b22;
  margin-bottom: 1px;
  margin-top: 1px;
}

  .contribution-cell.level-1 { background-color: #0e4429; }
  .contribution-cell.level-2 { background-color: #006d32; }
  .contribution-cell.level-3 { background-color: #26a641; }
  .contribution-cell.level-4 { background-color: #39d353; }

  .day-labels {
  
  display: flex;
  flex-direction: column;
  gap: 4px;
  font-size: 12px;
  margin-top: 3px;
  margin-right: 3px;
  order: -1; 
}

.legend {
    position: absolute;
    bottom: 0;
    right: 0;
    transform: translateY(100%);
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    font-size: 9px;
    color: #8b949e;
  }

  .legend-item {
    display: flex;
    align-items: center;
    margin-bottom: 4px;
  }

  .legend-color {
    width: 10px;
    height: 10px;
    border-radius: 2px;
    margin-right: 4px;
    background-color: #161b22;
    margin-bottom: 4px;
  }

  .legend-text {
    margin-left: 4px;
    display: flex;
    align-items: center;
  }

  .legend-color.level-4 { background-color: #39d353; }
</style>

<div class="github-contributions">
  <div class="contributions-header">GitHub contributions this year: {totalContributions}</div>
  <div class="contributions-container">
    <div class="day-labels">
      <span>Mon</span>
      <span>Wed</span>
      <span>Fri</span>
    </div>

    {#each weeks as week}
      <div class="week-container">
        {#each week as contribution}
          <div class="contribution-cell level-{contribution?.level || 0}"
               title="{contribution?.count || 0} contributions on {contribution?.month || ''} {contribution?.day || ''}">
          </div>
        {/each}
      </div>
    {/each}
  </div>

  <div class="legend">
    <div class="legend-item">
      <div class="legend-color level-0"></div>
      <span>Less</span>
    </div>
    <div class="legend-item">
      <div class="legend-color level-4"></div>
      <span>More</span>
    </div>
  </div>
</div>
