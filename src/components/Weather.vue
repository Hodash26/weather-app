<template>
    <div class="weather">
        <h2>
            Météo du {{ date | formatDate }}
        </h2>
        <div class="wrap">
            <div class="infos" v-if="infos">
                <p class="day">Maintenant</p>
                <p class="city">
                    {{infos.city.name}}
                </p>
                <p class="cloud">
                    <img  v-bind:src="changeimage0" alt="image du temps">
                </p>
                <p class="temp">
                    Temperature : {{ infos.list[0].main.temp}}°
                </p>
                <p class="humidity">
                    Taux d'humidité: {{infos.list[0].main.humidity}}%
                </p>
                <p class="wind">
                    Vitesse du vent : {{infos.list[0].wind.speed}}km/h
                </p>
            </div>
    
            <div class="infos" v-if="infos">
                <p class="day">Demain</p>
                <p class="city">
                    {{infos.city.name}}
                </p>
                <p class="cloud">
                    <img  v-bind:src="changeimage1" alt="image du temps">
                </p>
                <p class="temp">
                    Temperature : {{ infos.list[7].main.temp}}°
                </p>
                <p class="humidity">
                    Taux d'humidité: {{infos.list[7].main.humidity}}%
                </p>
                <p class="wind">
                    Vitesse du vent : {{infos.list[7].wind.speed}}km/h
                </p>
            </div>
    
            <div class="infos" v-if="infos">
                <p class="day">Après-demain</p>
                <p class="city">
                    {{infos.city.name}}
                </p>
                <p class="cloud">
                    <img  v-bind:src="changeimage2" alt="image du temps">
                </p>
                <p class="temp">
                    Temperature : {{ infos.list[15].main.temp}}°
                </p>
                <p class="humidity">
                    Taux d'humidité: {{infos.list[15].main.humidity}}%
                </p>
                <p class="wind">
                    Vitesse du vent : {{infos.list[15].wind.speed}}km/h
                </p>
            </div>
    
    
            <div class="infos" v-if="infos">
                <p class="day">Dans 3 jours</p>
                <p class="city">
                    {{infos.city.name}}
                </p>
                <p class="cloud">
                    <img  v-bind:src="changeimage3" alt="image du temps">
                </p>
                <p class="temp">
                    Temperature : {{ infos.list[23].main.temp}}°
                </p>
                <p class="humidity">
                    Taux d'humidité: {{infos.list[23].main.humidity}}%
                </p>
                <p class="wind">
                    Vitesse du vent : {{infos.list[23].wind.speed}}km/h
                </p>
            </div>
        </div>
        </div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'


export default {
    name: "Weather",
    data: function()
    {
        return {
            infos: null,
            date: null
        }
    },
    methods: {
        updateDate() {
            this.date = moment()
        }
    },
    computed: {
        changeimage0: function() {
            return this.infos ? 'https://openweathermap.org/img/wn/'+this.infos.list[0].weather[0].icon+'@2x.png' : '';
        },
        changeimage1: function() {
            return this.infos ? 'https://openweathermap.org/img/wn/'+this.infos.list[7].weather[0].icon+'@2x.png' : "";
        },
        changeimage2: function() {
            return this.infos ? 'https://openweathermap.org/img/wn/'+this.infos.list[15].weather[0].icon+'@2x.png' : "";
        },
        changeimage3: function() {
            return this.infos ? 'https://openweathermap.org/img/wn/'+this.infos.list[23].weather[0].icon+'@2x.png': "";
        }
    },
    created() {
        this.date = moment();
        setInterval(() => {this.updateDate()},1000)
        axios
            .get("https://api.openweathermap.org/data/2.5/forecast?q=Essars&units=metric&APPID=8ce918844b53476fc2c0fae219e82d75")
            .then(response => (this.infos = response.data))
    }
}
</script>

<style>
    html {
        background-image: url('../assets/background1.jpeg');
        background-repeat: no-repeat;
        background-size: 100%;
    }

    h2 {
        font-size: 40px;
        text-align: center;
    }

    .city {
        font-size: 24px;
    }

    .day {
        font-size: 25px;
        font-weight: bold;
        font-family:sans-serif
    }

    .infos {
        text-align:center;
        color: black;
        border: 2px dashed black;
        font-size: 19px;
        width: 40%;
        margin: 15px;
        }

    .wrap {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        width: 100%;
    }

    .cloud {
        margin:0;
    }

    img {
        height: 150px;
        width: 150px;
        background-color: black; 
    }
</style>