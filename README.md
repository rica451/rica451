### English learderboard, v2

<sup>Last updated: 2024-11-24 18:17:40</sup>


<div class="selector-container" style="display: flex; align-items: center;">
  <label for="weightSelector"><sup>Score weights:</sup> </label>
  <select id="weightSelector" onchange="updateVisibility()" class="weight-select">
    <option value="0.333_0.333_0.333" selected>character: 1, entertain: 1, fluency: 1</option>
    <option value="0.25_0.5_0.25">character: 1, entertain: 2, fluency: 1</option>
    <option value="0.5_0.25_0.25">character: 2, entertain: 1, fluency: 1</option>
    <option value="0.25_0.25_0.5">character: 1, entertain: 1, fluency: 2</option>
  </select>
  <style>
  .weight-select {
    padding: 3px;
    margin: 0 0 0 3px;
    font-family: monospace;
    background: #2D2D2D;
    color: #B5B5B5;
    border: 1px solid #404040;
    border-radius: 3px;
    line-height: 1
    height: 20px;
  }
  .weight-select option {
    background: #2D2D2D;
    color: #B5B5B5;
  }
  sub[data-weight]:not([data-weight="0.333_0.333_0.333"]) {
    display: none;
  }
  </style>

  <script>
    function updateVisibility() {
      const selected = document.getElementById('weightSelector').value;
      document.querySelectorAll('sub[data-weight]').forEach(sub => {
        sub.hidden = sub.dataset.weight !== selected;
      });

      document.querySelectorAll('th:has(sub[data-weight])').forEach(th => {
        const hasSelectedWeight = th.querySelector(`sub[data-weight="${selected}"]`);
        const columnIndex = Array.from(th.parentElement.children).indexOf(th);
        if (columnIndex > -1) {
          document.querySelectorAll(`tr td:nth-child(${columnIndex + 1})`).forEach(td => {
            td.style.display = hasSelectedWeight ? 'table-cell' : 'none';
          });
          th.style.display = hasSelectedWeight ? 'table-cell' : 'none';

          if (hasSelectedWeight && th.textContent.includes('Length norm score')) {
            const tbody = th.closest('table').querySelector('tbody');
            const rows = Array.from(tbody.querySelectorAll('tr'));
            rows.sort((a, b) => {
              const aValue = parseFloat(a.children[columnIndex].textContent);
              const bValue = parseFloat(b.children[columnIndex].textContent);
              return bValue - aValue;
            });
            tbody.innerHTML = '';
            rows.forEach(row => tbody.appendChild(row));
          }
        }
      });
    }
    document.addEventListener('DOMContentLoaded', updateVisibility);
  </script>
</div>


|   # | Model name                                                      | Length norm score<sub data-weight="0.333_0.333_0.333"></sub>   | Length norm score<sub data-weight="0.25_0.5_0.25"></sub>   | Length norm score<sub data-weight="0.5_0.25_0.25"></sub>   | Length norm score<sub data-weight="0.25_0.25_0.5"></sub>   | Avg score<sub data-weight="0.333_0.333_0.333"></sub>     | Avg score<sub data-weight="0.25_0.5_0.25"></sub>         | Avg score<sub data-weight="0.5_0.25_0.25"></sub>         | Avg score<sub data-weight="0.25_0.25_0.5"></sub>         |   Refusal ratio |   Stay in character score |   Language fluency score |   Entertain score |   Num cases |   Avg length |
|-----|-----------------------------------------------------------------|---------------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|---------------------------------|---------------------------------|---------------------------------|---------------------------------|-----------------|---------------------------|--------------------------|-------------------|-------------|--------------|
|   1 | [11_29_judge]({{ '/results/v3/en/11_29_judge' | relative_url}}) | 4.73<sub><sup>±0.10</sup></sub>       | 4.67<sub><sup>±0.12</sup></sub>   | 4.74<sub><sup>±0.11</sup></sub>   | 4.80<sub><sup>±0.08</sup></sub>   | 4.73<sub><sup>±0.11</sup></sub> | 4.67<sub><sup>±0.12</sup></sub> | 4.74<sub><sup>±0.12</sup></sub> | 4.80<sub><sup>±0.07</sup></sub> |            0.00 |                      4.75 |                     5.00 |              4.46 |          63 |          401 |
