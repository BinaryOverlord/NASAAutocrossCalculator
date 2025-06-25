<script setup lang="ts">

</script >


<template>
  <div class="heading">
    <h1>NASA Autocross Class Calculator</h1>
  </div>

  <div class="container"> 
    <div class="header">
      Chassis and Suspension
    </div>
    <div class="rule">
      <div>Height Adjustabled Coil-overs</div>
      <div>25 </div>
      <div>
      <input type="checkbox">
      </div>
    </div>
    <div class="rule">
      <div>Springs Stage 1 (OEM style: Up to 30% rate increase and/or lowered 25mm or less) </div>
      <div>7</div>
      <div><input type="checkbox"></div>
    </div>
    <div class="rule">
      <div>Springs Stage 2 (Any spring combination beyond Stage 1) </div>
      <div>13</div>
      <div><input type="checkbox"></div>
    </div>
    <div class="rule">
      <div>Seam weld</div>
      <div>10</div>
      <div><input type="checkbox"></div>
    </div>
    <div class="rule">
      <div>Change Suspension Type and/or alternate mounting points.</div>
      <div>10</div>
      <div><input type="checkbox"></div>
    </div>
    <div class="rule">
      <div>Roll cage / Chassis Bracing (6 or mor attachment points)</div>
      <div>5</div>
      <div><input type="checkbox"></div>
    </div>
    <div class="rule">
      <div>Sway bars (1 bar, no points for modification to the bar and links)</div>
      <div>2</div>
      <div><input type="checkbox"></div>
    </div>
    <div class="rule">
      <div>Sway bars (both, no points for modification to the bar and links)</div>
      <div>6</div>
      <div><input type="checkbox"></div>
    </div>
  </div> 

  

</template>

<style>
@media (min-width: 1024px) {
  .heading {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}

  .rule {
    display: grid;
    grid-template-columns: auto 50px 50px;
  }

  .header {
    grid-row: 1;
    grid-column: 1 / span 3;
  }
</style>
