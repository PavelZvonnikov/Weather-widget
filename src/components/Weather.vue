<template>
  <div class="weather">
      <div class="weather__temp elem">
        <img class="logo" src="../assets/temp.svg" alt="">
        <p>Температура: <span class="text" :class="{blue: obj.active}"> {{obj.temp}} &#8451</span></p>
      </div>
      <div class="weather__press elem">
        <img class="logo" src="../assets/pressure.svg" alt="">
        <p>Давление: <span class="text" :class="{blue: obj.active}"> {{obj.pressure}} мм. рт. ст.</span></p>
      </div>
      <div class="weather__sunset elem">
        <img class="logo" src="../assets/sunset.svg" alt="">
        <p>Заход солнца: <span class="text" :class="{blue: obj.active}"> {{obj.sunset}} </span></p>
      </div> 
  </div>   
</template>

<script>
export default {
  name: 'Weather',
  props: {
    obj: Object,
  },
}

</script>

<style lang="scss">
  .weather {
    display: flex;
    flex-direction: column;
  }
  .logo {
    width: 40px;
    margin-right: 15px;
  }
  .elem {
    display: flex;
    height: 30px;
    font-size: 20px;
    margin-bottom: 25px; 
  }
  p {
    align-self: center;
  }
  .text {
    color: #A5A5A5;
  }

  li {
    list-style-type: none; 
  }
  .blue {
    color: #419BF4;
  }
</style>
