<template>
  <div class="wrapper">
    <div class="main">
      <div class="info">
        <Info />
      </div>
      <div class="form">
        <div class="form__center">
          <Form 
            :weatherMethod="gettingWeather" 
            :inputChange="inputChange"
            :remove="remove" 
            :city="city"
          />
          <Weather :obj="obj"/>
        </div>
      </div>
    </div>  
  </div>  
</template>

<script>
import Info from './components/Info.vue';
import Form from './components/Form.vue';
import Weather from './components/Weather.vue';

export default {
  name: 'app',
  components: {
    Info,
    Form,
    Weather
  },
  data() {
    return {
      obj: {
        temp: 0,
        pressure: '0:00:00',
        sunset: 0,
        active: false,
      },
      key: '23fbf964c1eb2fa295dd50b21b675122',
      city: '',
    }
  },
  methods: {
    gettingWeather: async function (e) {
      e.preventDefault();
      if (this.city) {
        const link = await 
        fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.key}&units=metric`);
        const data = await link.json();

        const synSunset = data.sys.sunset;

        const date = new Date(synSunset * 1000);
        const sunset = `${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`;

        this.obj.temp = data.main.temp;
        this.obj.data = data.name;
        this.obj.pressure = Math.round(data.main.pressure * 0.75006375541921);
        this.obj.sunset = sunset;
        this.obj.active = true;
      } 
    },
    inputChange: function (e) {
      this.city = e.target.value;
    },
    remove() {
      this.city = '';
      this.obj.temp = 0;
      this.obj.pressure = 0;
      this.obj.sunset = '0:00:00';
      this.obj.active = false;
    },
  },
}
</script>

<style lang="scss">
  .wrapper {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;

    background: rgba(45,176,224,1);
    background: -moz-linear-gradient(45deg, rgba(45,176,224,1) 0%, rgba(96,40,168,1) 100%);
    background: -webkit-gradient(left bottom, right top, color-stop(0%, rgba(45,176,224,1)), color-stop(100%, rgba(96,40,168,1)));
    background: -webkit-linear-gradient(45deg, rgba(45,176,224,1) 0%, rgba(96,40,168,1) 100%);
    background: -o-linear-gradient(45deg, rgba(45,176,224,1) 0%, rgba(96,40,168,1) 100%);
    background: -ms-linear-gradient(45deg, rgba(45,176,224,1) 0%, rgba(96,40,168,1) 100%);
    background: linear-gradient(45deg, rgba(45,176,224,1) 0%, rgba(96,40,168,1) 100%);
    filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#2db0e0', endColorstr='#6028a8', GradientType=1 );
  }

  .main {
    height: 320px;
    display: flex;
    background: #ffffff;
    box-shadow: 0px 2px 80px -20px rgba(0,0,0,0.5);
    width: 845px;
    margin: 0 auto;
    border-radius: 12px;
    border: 0;
    font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .info {
    height: 320px;
    width: 310px;
    background: url("./assets/img.png") center center no-repeat;
    background-size: cover;
    border-radius: 12px 0 0 12px;
    display: flex;
    flex-direction: column;
    text-align: center;
    color: #ffffff;
  }
  .form {
    width: 535px;
    display: flex;
    justify-content: center;
    
    &__center {
      display: flex;
      flex-direction: column;
    }
  }

</style>
