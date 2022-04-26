<template>
    <div class="center">
        <button style="margin-right: 1%" @click.prevent="changeGroupe('A')">
            <router-link :to="{ name: 'groupeA', params: { Etudiants: getEtudiants() }}">Groupe A</router-link>
        </button>
        <button style="margin-left: 1%, margin-right: 1%" @click.prevent="changeGroupe('B')">
            <router-link :to="{ name: 'groupeB', params: { Etudiants: getEtudiants() }}">Groupe B</router-link>
        </button>
        <button style="margin-left: 1%" @click.prevent="changeGroupe('AB')">
            <router-link :to="{ name: 'groupeAB', params: { Etudiants: getEtudiants() }}">Groupe A et B</router-link>
        </button>
    </div>
    <form @submit.prevent="add">
        <h3>Ajouter un étudiant</h3>
        <div class="center">
            <div>
                <label>ID</label> 
                <br>
                <input type="number" min="0" placeholder="ID nouveau étudiant" v-model.trim.lazy="nv_id" required>
            </div>
            <div>
                <label>Nom</label> 
                <br> 
                <input type="text" placeholder="Nom nouveau étudiant" v-model.trim.lazy="nv_nom" required>
            </div>
            <div>
                <label>Note</label> 
                <br> 
                <input type="number" max="20" min="0" placeholder="Note nouveau étudiant" v-model.trim.lazy="nv_note" required>
            </div>
            <div>
                <label>Groupe</label> 
                <br> 
                <select v-model.trim.lazy="nv_groupe">
                    <option>A</option>
                    <option>B</option>    
                </select>
            </div> 
        </div>
        <button type="submit" style="margin-top: 2%">Ajouter</button>
    </form>
  <router-view/>
</template>
<script>
export default {
    name: 'Exercice-2',
    data() {
        return {
            group_selected: 'A',
            nv_id: null,
            nv_nom: null,
            nv_note: null,
            nv_groupe: null,
            etudiants: [
                        {
                            id_etudiant : 20210001, 
                            nom : "Jessica", 
                            note : 18.9, 
                            groupe: "A"
                        },
                        {
                            id_etudiant : 20210002,
                            nom : "Joe", 
                            note : 8.2, 
                            groupe : "B"
                        },
                        {
                            id_etudiant : 20210003,
                            nom : "Keithley", 
                            note : 14.0, 
                            groupe : "B"
                        },
                        {
                            id_etudiant : 20210004,
                            nom : "Nela", 
                            note : 16.5, 
                            groupe : "A"
                        },
                        {
                            id_etudiant : 20210005,
                            nom : "Kemberly", 
                            note : 18.1, 
                            groupe : "B"
                        }
                    ]
        }
    },
    methods: {
        getEtudiants(){
            return JSON.stringify(this.etudiants)
        },
        changeGroupe(nvGroupe){
            this.group_selected = nvGroupe
        },
        add(){
            this.etudiants.push({"id_etudiant": this.nv_id, "nom": this.nv_nom, "note": parseInt(this.nv_note), "groupe": this.nv_groupe})
            this.nv_id = null
            this.nv_nom = null
            this.nv_note = null
            this.nv_groupe = null
            this.$router.push({ name: 'exercice2'})
        }
    }
}
</script>
<style>
.center{
    display: flex;
    justify-content: center;
    align-items: center;
}
.center div{
    margin-left: 2%
}

</style>

