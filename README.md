# weather-detaction
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather</title>

    <link rel="stylesheet" href="pot.css">

    

</head>
<body>
    
    <div class="card"> 
        <div class="search">
            <input type="text" placeholder="enter city name"
            spellcheck="false">
            <button><img src="images.png" ></button>
        </div>
        <div class="error">
            <p>Invalid City</p>
        </div>
        <div class="weather">
            <img src="sun.png" class="weather-icon">
            <h1 class="temp">21°C</h1>
            <h2 class="city">Ghaziabad</h2>
            <div class="details">
                <div class="col">
                    <img src="humidity (1).png"  >
                    <div>
                        <p class="humidity">50%</p>
                        <p>Humidity</p>
                    </div>
                </div>
                <div class="col">
                    <img src="wind.png"  >
                    <div>
                        <p class="wind">15km/h</p>
                        <p>Wind speed</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>

        const apikey="b89173c2c053cfe10050b95a8b53159b";
        const apiUrl="https://api.openweathermap.org/data/2.5/weather?units=metric&q=";

        const searchBox =document.querySelector(".search input");
        const searchBtn =document.querySelector(".search button");
        const weatherIcon = document.querySelector(".weather-icon");


        async function checkWeather(city) {

          const r= await fetch( apiUrl + city + `&appid=${apikey}`)  ;
          if(r.status==404)
          {
            document.querySelector(".error").style.display="block";
            document.querySelector(".weather").style.display="none";
          } 
          var data =await r.json();

        

          document.querySelector(".city").innerHTML = data.name;
          document.querySelector(".temp").innerHTML = Math.round(data.main.temp) + "°C";
          document.querySelector(".humidity").innerHTML = data.main.humidity + "%";
          document.querySelector(".wind").innerHTML = data.wind.speed +"km/h";

       


        document.querySelector(".weather").style.display="block";
    }

        searchBtn.addEventListener("click", ()=>{
            checkWeather(searchBox.value);
        })
        
    </script>

</body>
</html>

/# css file
*{
    margin: 0;
    padding: 0;
    font-family: 'Poppins',sans-serif;
    box-sizing: border-box;
}

body{
    background:#222 ;
}

.card
{
    width:90%;
    max-width: 470px;
    background: linear-gradient(135deg, #00feba, #5b548a);
    color: #fff;
    margin: 100px auto 0;
    border-radius: 20px;
    padding: 40px 35px;
    text-align: center;
}

.search{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.search input{
    border: 0;
    outline: 0;
    background: #ebfffc;
    color: #555;
    padding: 10px 25px;
    height: 60px;
    border-radius: 30px;
    flex: 1;
    margin-right: 16px;
    font-size: 18px;
}

.search button
{
    border: 0;
    outline: 0;
    background: #ebfffc;
    border-radius: 50%;
    width: 60px;
    height: 60px;
    cursor: pointer;
}
.search button img{
    width: 16px;
}
.weather{
    display: none;
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

.col
{
    display: flex;
    align-items: center;
    text-align: left;
}
.col img{
    width: 40px;
    margin-right:10px ;
}
.humidity, .wind{
    font-size: 28px;
    margin-top: -6px;
}
.error{
    text-align: left;
    margin-left: 10px;
    font-size: 14px;
    margin-top: 10px;
    display: none;
}
