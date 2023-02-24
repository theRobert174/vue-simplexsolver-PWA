<template>
    <h1>Simplex Solver</h1>
    <ion-grid style="height: 100%">
        <ion-row style="height: 100%; justify-content: center; align-items: center;">
            <ion-card>
                <form-equation></form-equation>
            </ion-card>
        </ion-row>
        <ion-row style="height: 100%; justify-content: center; align-items: center;">
            <ion-card>
                <ion-card-header>
                    <ion-card-title style="font-weight: bold;"><h2>Tablero 1</h2></ion-card-title>
                </ion-card-header>
                <ion-card-content>
                    <my-table :rows="5" :cols="10"></my-table>
                </ion-card-content>
            </ion-card>
        </ion-row>
    </ion-grid>
</template>

<script>
/* eslint-disable*/
import { IonCard, IonGrid, IonRow, IonCol, IonItem, IonSelect, IonSelectOption, IonLabel, IonList } from '@ionic/vue';
import MyTable from '@/components/Table.vue'
import FormEquation from '@/components/FormEquation.vue'
export default {
        name: 'TableView',
        components: {
        IonCard,
        IonGrid,
        IonRow,
        IonCol,
        IonList,
        IonItem,
        IonSelect,
        IonSelectOption,
        IonLabel,
        MyTable,
        FormEquation
    },
    data(){
        return{

        }
    },
    methods: {
        
    },
}
</script>

<style scoped>

</style>