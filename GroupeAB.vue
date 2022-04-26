<template>
    <div class="center" style="margin-top: 2%">
        <table>
            <caption>Etudiants du groupe A et B</caption>
            <thead>
                <tr>
                    <th>Id étudiant</th>
                    <th>Nom</th>
                    <th>Note</th>
                    <th>Groupe</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="etudiant in etudiants" v-bind:key="etudiant.id_etudiant">
                    <td>{{etudiant.id_etudiant}}</td>
                    <td>{{etudiant.nom}}</td>
                    <td>{{etudiant.note}}</td>
                    <td>{{etudiant.groupe}}</td>
                </tr>
            </tbody>
        </table>
    </div>
    <h3>La moyenne de tous les étudiants est de : {{moyenne}}</h3>
    <h3>La note maximale de tous les étudiants est de {{noteMax}} de l'étudiant {{etudiantMax}}</h3>
</template>
<script>
export default {
    name: 'GroupeAB',
    data() {
        return {
            etudiants: this.sortEtudiants(JSON.parse(this.$route.params.Etudiants))
        }
    },
    methods: {
        sortEtudiants(etudiants){
            return etudiants.sort((e1, e2) => {
                return e1.groupe < e2.groupe ? -1 : e1.groupe > e2.groupe ? 1 : 0
            })
        }
    },
    computed: {
        moyenne() {
            var total = 0
            this.etudiants.forEach(e => {
                total += e.note
            });
            return (Math.round((total/this.etudiants.length) * 100) / 100).toFixed(2);
        },
        noteMax() {
            var noteMax = this.etudiants[0].note
            for(var i = 0 ; i < this.etudiants.length ; i++)
                if(this.etudiants[i].note > noteMax)
                    noteMax = this.etudiants[i].note
            return noteMax
        },
        etudiantMax() {
            var indexMax = 0
            for(var i = 0 ; i < this.etudiants.length ; i++)
                if(this.etudiants[i].note > this.etudiants[indexMax].note)
                    indexMax = i
            return this.etudiants[indexMax].nom
        }
    }
}
</script>