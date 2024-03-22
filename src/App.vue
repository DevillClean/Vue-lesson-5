<script>

import axios from 'axios'
export default {
  data(){
    return{
      city:'',
      error:'',
      info: null
    }
  },
  computed:{
    cityName(){
      return "«" + this.city + "»"
    },
    showTemp(){
      return "Температура :" + this.info.main.temp
    },
    showFeelsLike(){
      return "Ощущаеться как :" + this.info.main.feels_like
    },
    showMaxTemp(){
      return "Максимальная температура :" + this.info.main.temp_max
    },
  },
  methods:{
    getWeather(){
      if(this.city.trim().length < 2){
        this.error = "Нужно название больше одного символа"
        return false
      }
      this.error = ""

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=1e0a068ed11d94f91ed9fac839881218`)
          .then(res => (this.info = res.data))
    }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>Приложение с погодой </h1>
    <p>Узнать погоду в {{city == '' ? ' городе' : cityName}}</p>
    <input type="text" v-model="city" placeholder="Введіть місто">
    <button v-if="city != ''" @click="getWeather">Получить результат</button>
    <button disabled v-else>Введите название города</button>
    <p class="error"> {{error}}</p>


    <div v-if="info != null">
    <p>{{showTemp}}</p>
      <p>{{showFeelsLike}}</p>
      <p>{{showMaxTemp}}</p>
    </div>

  </div>


</template>

<style scoped>
.error{
  color: red;
}

.wrapper{
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #4a65eb;
  text-align: center;
  color: white;
}
.wrapper h1{
  margin-top: 50px;
}
.wrapper p{
  margin-top: 20px;
}
.wrapper input{
  margin-top: 30px;
  background: #4b59a7;
  border: 0;
  border-bottom: 2px solid #565656;

  font-size: 16px;
  padding: 5px 8px;
  outline: none;
}
.wrapper input:focus{
  border-bottom-color: #080101;
}

.wrapper button{
  background: #2648fb;
  color: white;
  border-radius: 10px;
  border: 2px solid #162eab;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:hover{
  transform: scale(1.1) translateY(-5px);
}

.wrapper button:disabled{
  cursor: not-allowed;
}


</style>
