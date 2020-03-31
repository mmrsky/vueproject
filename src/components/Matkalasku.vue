<template>
    <div class="matkalasku">
        <h1>{{ title }}</h1>

        <h4>Anna matkan alkuajankohta</h4>
        <input type="date" name="" value="" v-model="startDate">
        <!-- <input type="time" name="" value="" v-model="startTime"> -->
        <h4>Anna matkan loppuajankohta</h4>
        <input type="date" name="" value="" v-model="endDate">
        <!-- <input type="time" name="" value="" v-model="endTime"> -->
        <h4>Valitse kohdemaa</h4>
        <select v-model="selected">
            <option v-for="country in countries" v-bind:key="country.id">
                {{ country.text }}
            </option>
        </select>
        <span>Päiväraha: {{ selected }}</span>    
        <h6>{{ answer }}</h6>
        <br>
        <button type="button" name="button" @click="calculateAllowances(startDate, endDate, selected)">Laske</button>
    </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)

export default {
    name: 'Matkalasku',
    props: {
        msg: String
    },
    data: function() {
        return {
            answer: '',
            title: "Päivärahalaskuri",
            countries: [],
            selected: '',
            startDate: Date(),
            endDate: Date()
            //startTime: '0',
            //endTime: '1'
        };
    },
    methods: {
        getCountryData: function () {
          axios.get('http://localhost:8081/api')
          //axios.get('http://mlbe.herokuapp.com/api')
            .then( (response) => {  
                this.countries = response.data;
            })
            .catch( (error) => {
                this.answer = 'Virhe! Rajapintaan ei saada yhteyttä. ' + error
                console.log(error);
            });
        },
        // Lasketaan päivärahat annettujen tietojen pohjalta
        calculateAllowances: function (startDate,endDate,selected) { //,startTime,endTime) {
            console.log(selected);
            var years = parseInt(endDate.substring(0,4) - startDate.substring(0,4));
            var startMonth = parseInt(startDate.substring(5,7));
            var endMonth = parseInt(endDate.substring(5,7));
            var startDay = parseInt(startDate.substring(8,10));
            var endDay = parseInt(endDate.substring(8,10));
            var months = (((years * 12) + endMonth) - startMonth);// + ((years-1)*365);
            var days = ((months * 30) + endDay) - startDay; // Oikaistaan mutkia ja oletetaan että kuukaudessa on 30 päivää
            console.log('days2 ' + days);
            //var allowanceTotal = 0;

            //console.log(allowanceTotal);
        },


    },
    mounted: function (){
        this.getCountryData();
    }  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
