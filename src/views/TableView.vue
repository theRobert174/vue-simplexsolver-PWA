<template>
    <h1>Simplex Solver</h1>
    <ion-grid style="height: 100%">
        <ion-row style="height: 100%; justify-content: center; align-items: center;">
            <ion-card>
                <div class="container-func">
                    <ion-label for="opt">P: </ion-label>
                    <select id="opt" v-model="selectedOption" name="opt" style="margin-right: 1rem;">
                        <option value="min">min</option>
                        <option value="max">max</option>
                    </select>

                    <ion-label for="inputs"> z=</ion-label>
                    <div v-for="(input, index) in inputs" :key="input.id" class="input-container">
                        <span v-if="index === 0">&nbsp;&nbsp;</span>
                        <span v-else>+</span>
                        <input
                            :id="'input-' + input.id"
                            type="text"
                            v-model="input.value"
                            @input="adjustWidth($event.target)"
                            @keydown.enter="addInput(index + 1)"
                            @keydown.right="addInput(index + 1)"
                            ref="inputRefs"
                            :style="{ 'min-width': '5px', 'width': input.width + 'px' }"
                        />
                        <label :for="'input-' + input.id">x<sub>{{ input.id }}</sub></label>
                    </div>
                </div>
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
        MyTable
    },
    data(){
        return{
            selectedOption: 'min',
            inputs: [
                {
                    id: 1,
                    value: ''
                },
                {
                    id: 2,
                    value: ''
                }
            ]
        }
    },
    methods: {
        addInput(index) {
            if (this.inputs[index - 1].value !== '' && index <= 9) {
                const newId = this.inputs.length + 1;
                const newInput = {
                    id: newId,
                    value: ''
                };
                this.inputs.splice(index, 0, newInput);
                this.$nextTick(() => {
                    this.$refs.inputRefs[index].focus();
                });
            }
        },
        adjustWidth(input) {
            input.style.width = '1px';
            input.style.width = `${input.scrollWidth}px`;
        }
    },
}
</script>

<style scoped>

.container-func {
  display: flex; /* Alineamos los elementos en fila */
  align-items: center; /* Centramos verticalmente los elementos */
}
input{
    margin-right: 5px;
}
.input-container {
    display: flex;
}
.input-container input {
    width: 1ch;
    min-width: 50px; /* o cualquier otro valor que funcione para tu caso específico */
    margin-right: 5px;
}
</style>