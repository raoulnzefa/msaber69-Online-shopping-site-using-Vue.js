<template>
    <div class="center" style="margin-top: 2%">
        <table>
            <caption>Etudiants du groupe B</caption>
            <thead>
                <tr>
                    <th>Id étudiant</th>
                    <th>Nom</th>
                    <th>Note</th>
                    <th>Groupe</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="etudiant in etudiantsB" v-bind:key="etudiant.id_etudiant">
                    <td>{{etudiant.id_etudiant}}</td>
                    <td>{{etudiant.nom}}</td>
                    <td>{{etudiant.note}}</td>
                    <td>{{etudiant.groupe}}</td>
                </tr>
            </tbody>
        </table>
    </div>
    <h3>La moyenne des étudiants du groupe B est de : {{moyenne}}</h3>
    <h3>La note maximale des étudiants du groupe B est de {{noteMax}} de l'étudiant {{etudiantMax}}</h3>
</template>
<script>
export default {
    name: 'GroupeB',
    data() {
        return {
            etudiants: JSON.parse(this.$route.params.Etudiants)
        }
    },
    computed: {
        etudiantsB() {
            return this.etudiants.filter(e => {
                return e.groupe == 'B';
            })
        },
        moyenne() {
            var total = 0
            this.etudiantsB.forEach(e => {
                total += e.note
            });
            return (Math.round((total/this.etudiantsB.length) * 100) / 100).toFixed(2);
        },
        noteMax() {
            var noteMax = this.etudiantsB[0].note
            for(var i = 0 ; i < this.etudiantsB.length ; i++)
                if(this.etudiantsB[i].note > noteMax)
                    noteMax = this.etudiantsB[i].note
            return noteMax
        },
        etudiantMax() {
            var indexMax = 0
            for(var i = 0 ; i < this.etudiantsB.length ; i++)
                if(this.etudiantsB[i].note > this.etudiantsB[indexMax].note)
                    indexMax = i
            return this.etudiantsB[indexMax].nom
        }
    }
}
</script>