<template>
    
    <div class="container">
        
        <h1 class="my-4 text-center">Application Météo</h1>

        <div class="form-group mb-5">
            <label for="position">Entrez le Nom de votre Ville</label>
            <input 
            type="text" 
            id="position" 
            class="form-control"
            v-model="requette"
            v-on:keypress="goMeteo">
        </div>

        <div class="w-75 m-auto" v-if="temps">
            <h3 class="text-center mb-4 ma-pos">Position : {{ temps.name }}</h3>
            <div class="card text-center p-5 ma-card">
                <!-- toFixed() permet d'arrondir la température-->
                <p class="texte-affichage">Température : {{ temps.main.temp.toFixed() }}°</p>
                <p class="texte-affichage">Temps : {{ temps.weather[0].description }}</p>
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
    font-size: 26px;
    font-weight: 500;
    line-height: 1.5;
    font-family: 'Kaushan Script';
}
.ma-card {
    background: #1FA2FF;  /* fallback for old browsers */
    background: -webkit-linear-gradient(to right, #A6FFCB, #12D8FA, #1FA2FF);  /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(to right, #A6FFCB, #12D8FA, #1FA2FF); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

}
.ma-pos {
    background: #1FA2FF;  /* fallback for old browsers */
    background: -webkit-linear-gradient(to right, #A6FFCB, #12D8FA, #1FA2FF);  /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(to right, #A6FFCB, #12D8FA, #1FA2FF); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}



</style>