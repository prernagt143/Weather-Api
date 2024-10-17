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
