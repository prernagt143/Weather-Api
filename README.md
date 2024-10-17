# Weather-Api
Weather Api
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <link rel="stylesheet" href="weather.css">  
</head>
<body>
    <div class="card">
        <div class="search">
            <input type="text" placeholder="enter city name" spellcheck="false">
            <button><img src="search.png"></button>
        </div>
        <div class="error">
            <p>Invalid City Name</p>
        </div>
        <div class="weather">
            <img src="weather1.png" class="weather-icon">
            <h1 class="temp"> 22°c</h1>
            <h2 class="city">New York</h2>
            <div class="details">
                <div class="col">
                    <img src="humidity.png">
                    <div>
                        <p class="humidity">50%</p>
                        <p>Humidity</p>
                    </div>
                </div>
                <div class="col">
                    <img  src="wind.png">
                    <div>
                        <p class="wind">15 Km/h</p>
                        <p>Wind Speed</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
<script>
const apiKey = "3cd4cfffe5085d32d29293da02653a53";
const apiUrl = "https://api.openweathermap.org/data/2.5/weather?q="; 

const searchBox = document.querySelector(".search input");
const searchBtn = document.querySelector(".search button");
const weatherIcon = document.querySelector(".weather-icon");

async function checkWeather(city) {
    const response = await fetch(apiUrl + city + `&appid=${apiKey}&units=metric`); 

    if(response.status == 404){
        document.querySelector(".error").style.display = "block";
        document.querySelector(".weather").style.display = "none";
    }
    else{
        var data = await response.json();
        // console.log(data);

    document.querySelector(".city").innerHTML = data.name; 
    document.querySelector(".temp").innerHTML = Math.round(data.main.temp) + "°c"; 
    document.querySelector(".humidity").innerHTML = data.main.humidity + "%" ;
    document.querySelector(".wind").innerHTML = data.wind.speed + " Km/h"; 

    if(data.weather[0].main == "Clouds"){
        weatherIcon.src="cloudy.png";
    }
    else if(data.weather[0].main == "Clear"){
        weatherIcon.src="clear.png";
    }
    else if(data.weather[0].main == "Rain"){
        weatherIcon.src="rainy.png";
    }
    else if(data.weather[0].main == "Drizzle"){
        weatherIcon.src="dizzle.png";
    }
    else if(data.weather[0].main == "Mist"){
        weatherIcon.src="mist.png";
    }
    else if(data.weather[0].main == "Clear"){
        weatherIcon.src="clear.png";
    }

    document.querySelector(".weather").style.display = "block";
    document.querySelector(".error").style.display = "none";

    }
    }
searchBtn.addEventListener("click", ()=>{
    checkWeather(searchBox.value);
})
checkWeather();
</script>
</body>
</html>

* {
    margin: 0;
    padding: 0;
    font-family: 'Poppins', sans-serif;
    box-sizing: border-box;
}
body {
    background: #222;
}
.card {
    width: 90%;
    max-width: 470px; /* Changed from 470% to 470px for proper width */
    background: linear-gradient(135deg, #00feba, #5b548a);
    color: #fff;
    margin: 100px auto 0;
    border-radius: 20px;
    padding: 40px 35px;
    text-align: center;
}
.search {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.search input {
    border: 0;
    outline: 0;
    background: #ebfffc;
    color: #555;
    padding: 10px 25px;
    height: 60px;
    border-radius: 30px; /* Curvy corners */
    flex: 1;
    margin-right: 16px;
    font-size: 18px;
}
.search button {
    background: transparent;
    border: none;
    cursor: pointer;
}
.search button{
    border: 0;
    outline: 0;
    background: #ebfffc;
    border-radius: 50%;
    width: 60px;
    height: 60px;
    cursor: pointer;
}
.search button:hover {
    background: #babebd; 
    transform: scale(1.1);
}
.search button img{
    width: 16px;
}
.weather-icon{
    width: 170px;
    margin-top: 30px;
}
.weather h1{
    font-size: 80px;
    font-weight: 500;
}
.weather h2{
    font-size: 45px;
    font-weight: 400;
    margin-top: -10px;
}
.details{
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 20px;
    margin-top: 50px;

}
.col{
    display: flex;
    align-items: center;
    text-align: left;
}
.col img{
    width: 40px;
    margin-right: 10px;
}
.humidity, .wind{
    font-size:28px;
    margin-top: -6px;
}
.weather{
    display: none;
}
.error{
    text-align: left;
    margin-left: 10px;
    font-size: 14px;
    margin-top: 10px;
    display: none;
}
