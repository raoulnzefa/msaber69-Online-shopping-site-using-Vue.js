<template>
    <form @submit.prevent="sendMessage">
        <h2>Todo List</h2>
        <h3 style="font-weight: bold ; text-align: start ; text-decoration: underline">Ajouter un élément</h3>
        <p style="font-weight: lighter ; text-align: start">Titre</p>
        <input  type="text" placeholder="Donner un titre à votre Todo List" style="width: 100%; padding: 10px 18px; font-size: 18px; margin-bottom: 16px" v-model="titre" required>
        <br/>
        <p style="font-weight: lighter ; text-align: start">Description</p>
         <input  type="text" placeholder="Donner une description à votre Todo List" style="width: 100%; padding: 10px 18px; font-size: 18px; margin-bottom: 16px" required v-model="description"/>
         <br/>
         <div style="text-align: start">
         <label>Tâche déjà réalisée ?</label><input type="checkbox" id="tache?" v-model="fini" >
        </div>
         <button @click.prevent="add" >Ajouter la tache</button>
        <h3 style="font-weight: bold ; text-align: start ; text-decoration: underline">Liste</h3>
        <p style="font-weight: bold ; text-align: start ; text-decoration: underline">Tâches effectuées : {{vrai}}</p>
        <p style="font-weight: bold ; text-align: start ; text-decoration: underline">Tâches non-effectuées : {{faux}}</p>
    </form>
</template>
<script>
export default {
    name: 'AjouterTache',
    data  : function (){
        return {
            titre : '',
            description : '',
            fini : String.fromCodePoint(0x274C),
            vrai : 0,
            faux : 2

        }
    },
    methods : {
        add : function (){
         
            this.$emit('taskadded', {
                titre : this.titre,
                description : this.description,
                fini : this.fini
            } )
            if(this.fini === true){
                this.vrai += 1;
            }
            else{
                this.faux += 1;
            }

        }
    }
}
</script>