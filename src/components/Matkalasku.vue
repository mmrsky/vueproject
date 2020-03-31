<template>
    <div class="matkalasku">
        <h1>{{ title }}</h1>

        <h4>Anna matkan alkuajankohta</h4>
        <input type="date" name="" value="" v-model="startDate">
        <h4>Anna matkan loppuajankohta</h4>
        <input type="date" name="" value="" v-model="endDate">
        <h4>Valitse kohdemaa</h4>
        <select v-model="selected">
            <option v-for="country in countries" v-bind:key="country.id" v-bind:value="{id: country.id, name: country.name, value:country.value}">
                {{ country.name }}
            </option>
        </select>
        <span>Päiväraha: {{ selected.value }}</span>    
        <!-- <result-line></result-line> -->
        <h3>{{ answer }}</h3>
        <br>
        <button id="calcbutton" type="button" name="button" @click="calculateAllowances(startDate, endDate, selected.value)">Laske</button>
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
        };
    },
    methods: {
        // Haetaan maa ja päivärahatiedot palvelimelta
        getCountryData: function () {
          //axios.get('http://localhost:8081/api')
          axios.get('http://mlbe.herokuapp.com/api')
            .then( (response) => {  
                this.countries = response.data;
            })
            .catch( (error) => {
                this.answer = 'Virhe! Rajapintaan ei saada yhteyttä. ' + error
            });
        },
        // Lasketaan päivärahat annettujen tietojen pohjalta
        calculateAllowances: function (startDate,endDate,allowance) { 
            var years = parseInt(endDate.substring(0,4) - startDate.substring(0,4));
            var startMonth = parseInt(startDate.substring(5,7));
            var endMonth = parseInt(endDate.substring(5,7));
            var startDay = parseInt(startDate.substring(8,10));
            var endDay = parseInt(endDate.substring(8,10));
            var months = (((years * 12) + endMonth) - startMonth);
            var days = ((months * 30) + endDay) - startDay; // Oikaistaan mutkia ja oletetaan että kuukaudessa on 30 päivää

            if (!days)
            {
                this.answer = 'Tarkista että olet syöttänyt kaikki tiedot oikein!';
            }
            else
            {
                var allowanceTotal = days * allowance;
                this.answer = 'Päivärahan määrä on: ' + allowanceTotal + ' euroa';
            }
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

#calcbutton {
	box-shadow:inset 0px 1px 0px 0px #a4e271;
	background:linear-gradient(to bottom, #89c403 5%, #77a809 100%);
	background-color:#89c403;
	border-radius:6px;
	border:1px solid #74b807;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
	font-family:Arial;
	font-size:15px;
	font-weight:bold;
	padding:6px 24px;
	text-decoration:none;
	text-shadow:0px 1px 0px #528009;
  width: 250px;
}
#calcbutton:hover {
	background:linear-gradient(to bottom, #77a809 5%, #89c403 100%);
	background-color:#77a809;
}
#calcbutton:active {
	position:relative;
	top:1px;
}

</style>
