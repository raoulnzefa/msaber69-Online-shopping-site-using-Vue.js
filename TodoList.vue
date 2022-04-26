<template>
    <p>{{faux}}</p>
    <table class="datatable">
        <thead>
            <tr>
                <th>Titre</th>
                <th>Description</th>
                <th>Etat</th>
            </tr>
            <tr>
                <th>
                    <li v-for="t in taches" :key="t.titre" style="list-style-type: none">
                        <span v-if="t.titre === null">rien</span>
                        <span v-else>{{t.titre}}</span>
                    </li>
                </th>
                <th>
                    <li v-for="t in taches" :key="t.description" style="list-style-type: none">
                        <span>{{t.description}}</span>
                    </li>
                </th>
                <th>
                    <li v-for="t in taches" :key="t.fini" style="list-style-type: none">
                        <span v-if="t.fini === true">&#9989;</span>
                        <span v-else>&#10060;</span>
                    </li>
                </th>
            </tr>
        </thead>
    </table>
</template>
<script>
export default {
    name : 'TodoList',

    props : {
        taches : Array
    },
    data : function (){
        return {

        }
    }
}
</script>

<style scoped>

</style>