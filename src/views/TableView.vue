<template>
    <ion-grid style="height: 100%">
        <ion-row style="height: 100%; justify-content: center; align-items: center;">
            <ion-card>
                <ion-item>
                    <ion-label>P: </ion-label>
                    <ion-select value="min" placeholder="opt">
                        <ion-select-option value="min">min</ion-select-option>
                        <ion-select-option value="max">max</ion-select-option>
                    </ion-select>
                </ion-item>
                
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
import { IonCard, IonGrid, IonRow, IonCol, IonItem, IonSelect, IonSelectOption, IonLabel } from '@ionic/vue';
import Table from '@/components/Table.vue'
export default {
    name: 'TableView',
    components: {
    IonCard,
    IonGrid,
    IonRow,
    IonCol,
    IonItem,
    IonSelect,
    IonSelectOption,
    IonLabel,
    MyTable : Table
  }
}
</script>

<style scoped>

</style>