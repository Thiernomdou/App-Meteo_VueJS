<template>
    
    <div class="container">
        
        <h1 class="my-4 text-center">Application Météo</h1>

        <div class="form-group mb-5">
            <label for="position"><b>Entrez le Nom de votre Ville</b></label>
            <input 
            type="text" 
            id="position" 
            class="form-control"
            v-model="requette"
            v-on:keypress="goMeteo">
        </div>

        <div class="w-75 m-auto" v-if="temps">
            
            <div class="card text-center p-5 ma-card">
                <!-- toFixed() permet d'arrondir la température-->
                <p class="texte-affichage">{{ temps.name }}</p>
                <p class="texte-affichage">{{ temps.main.temp.toFixed() }}°</p>
                <p class="texte-affichage">{{ temps.weather[0].description }}</p>
            </div>
        </div>

    </div>

</template>

<script>
//axios permet de faire de requettes HTTP
import axios from 'axios'

export default {
    name: 'Meteo',
    data() {
        return {
            requette: '',
            temps: undefined,
            api_code: '6fbf739752280f9ef37af35f1534adbf',
            url_recherche: 'https://api.openweathermap.org/data/2.5/weather?'
        }
    },
    methods: {
        //qui va s'activer à chaque fois qu'on 
        // appuie sur des touches quand on est dans l'input
        goMeteo(e) {
            // Si tu cliques sur entrée
            if(e.key == "Enter") {

                axios
                // q signifie query(requette)
                //units=metric = que les unités metic, pas fareneith
                //APPID est notre clé secrète API
                .get(`${this.url_recherche}q=${this.requette}
                &units=metric&APPID=${this.api_code}&lang=fr`)
                // quand on reçoit notre reponse de l'API
                .then(reponse => {
                    // console.log(reponse);
                    this.temps = reponse.data;
                    // console.log(this.temps);
                })
                    this.requette = '';
            }
        }
    }
}
</script>

<style scoped>

.texte-affichage {
    font-size: 50px;
    font-weight: 500;
    line-height: 1.5;
}
.ma-card {
    background: transparent;
    border: none;
}




</style>