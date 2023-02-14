<template>

    <div id="weathercontainer" >
        
      <form>
        <div class="upperformarea">
            <label for="city col-sm-2 col-form-label">Enter City Name:   </label>
        <input type="text" id="city" name="city" placeholder=" City Name" class="form-control" required>
      
        </div>
         <br>
        <div class="button">
        <button v-on:click="getData()" type="submit">Submit</button>

        </div>
      </form>
      <div id="weatherResult"></div>
    </div>
    </template>

    <script >
   export default{
    name:'Main',
  
    
    methods: {
        getData(){
            
         
const form = document.querySelector('form');
const cityInput = document.querySelector('#city');
const weatherResult = document.querySelector('#weatherResult');

form.addEventListener('submit', (event) => {
  event.preventDefault();
  const city = cityInput.value;

  fetch(`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=de124e0feb0b49e610e4f15c412c81c8`)
    .then((response) => {
      return response.json();
    })
    .then((getdata) => {
        let temp = getdata.main.temp
        let updatedtemp = temp - 273.15 

         weatherResult.innerHTML = `
   
        <div class="data">
            <p>Temperature: ${parseFloat(updatedtemp).toFixed(2)}°C</p>
        <p>Humidity: ${getdata.main.humidity}%</p>
        <p>Weather: ${getdata.weather[0].description}</p>
        <p>Visibility: ${getdata.visibility}</p>
            </div>
      `;
      
    })
    .catch((error) => {
      weatherResult.innerHTML = '<p>Sorry City not found</p>';
    });
});
        }
    },
}
    </script>
    <style>
    *{
        font-family: sans-serif;
    }
label{
    color: aliceblue;
}
input{
   
    border-radius: 25px;
}
.button{
    display: flex;
    justify-content: center;
}
button{
    margin-top: 20px;
    padding: 8px 30px;
    border-top-left-radius: 20px;
    border-top-right-radius: 50px;
    border-bottom-left-radius: 50px;
    border-bottom-right-radius: 20px;
    cursor: pointer;
    background-color: aliceblue;
}
button:hover{
    background-color: #252525;
    color: aliceblue;
    border: 1px solid white;
    transition: 0.5s;
    padding: 8px 60px;
    font-weight: bold;
}
button:not(:hover){
    padding: 8px 30px;
    transition: 0.5s;

}
.data{
    margin-top: 20px;
    color: aliceblue;
    font-size: 18px;
    
    
}
  #weathercontainer{
    display: flex; 
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: 150px;
 }
 .upperformarea{
    display: flex;
    flex-direction: row;
 }
</style>
   