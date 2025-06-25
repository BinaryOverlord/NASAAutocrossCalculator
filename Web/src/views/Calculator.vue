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
