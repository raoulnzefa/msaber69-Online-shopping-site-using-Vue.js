<template>
    <div class="center" style="margin-top: 2%">
        <table>
            <caption>Etudiants du groupe A</caption>
            <thead>
                <tr>
                    <th>Id étudiant</th>
                    <th>Nom</th>
                    <th>Note</th>
                    <th>Groupe</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="etudiant in etudiantsA" v-bind:key="etudiant.id_etudiant">
                    <td>{{etudiant.id_etudiant}}</td>
                    <td>{{etudiant.nom}}</td>
                    <td>{{etudiant.note}}</td>
                    <td>{{etudiant.groupe}}</td>
                </tr>
            </tbody>
        </table>
    </div>
    <h3>La moyenne des étudiants du groupe A est de : {{moyenne}}</h3>
    <h3>La note maximale des étudiants du groupe A est de {{noteMax}} de l'étudiant {{etudiantMax}}</h3>
</template>
<script>
export default {
    name: 'GroupeA',
    data() {
        return {
            etudiants: JSON.parse(this.$route.params.Etudiants)
        }
    },
    computed: {
        etudiantsA() {
            return this.etudiants.filter(e => {
                return e.groupe == 'A';
            })
        },
        moyenne() {
            var total = 0
            this.etudiantsA.forEach(e => {
                total += e.note
            });
            return (Math.round((total/this.etudiantsA.length) * 100) / 100).toFixed(2);
        },
        noteMax() {
            var noteMax = this.etudiantsA[0].note
            for(var i = 0 ; i < this.etudiantsA.length ; i++)
                if(this.etudiantsA[i].note > noteMax)
                    noteMax = this.etudiantsA[i].note
            return noteMax
        },
        etudiantMax() {
            var indexMax = 0
            for(var i = 0 ; i < this.etudiantsA.length ; i++)
                if(this.etudiantsA[i].note > this.etudiantsA[indexMax].note)
                    indexMax = i
            return this.etudiantsA[indexMax].nom
        }
    }
}
</script>