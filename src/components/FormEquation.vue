<template>
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
                @keyup="onKeyUp(index,$event)"
                @keydown="onKeyDown(index,$event)"
                @keydown.right="addInput(index)"
                @keydown.backspace="deleteInput(index)"
                ref="inputRefs"
                :style="{ 'min-width': '5px', 'width': input.width + 'px' }"
            />
            <label :for="'input-' + input.id">x<sub>{{ input.id }}</sub></label>
        </div>
    </div>
</template>

<script>
import { IonLabel } from '@ionic/vue';
export default {
    name: 'FormEquation',
    components:{
        IonLabel
    },
    data(){
        return{
            selectedOption: 'min',
            delayI: -1,
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
        //Ajusta el grosor de cada input en relación a su contenido
        adjustWidth(input) {
            input.style.width = '1px';
            input.style.width = `${input.scrollWidth}px`;
        },
        //Añade un input al final del lado derecho
        addInput(index) {
            const inpAct = this.$refs.inputRefs[index]//input Actual
            //Si el input Actual no tiene nada o esta en la pos final y la cant de inputs es menor o igual a 9 y el total de inputs es igual a la cant existentes
            if ((inpAct.value === '' || inpAct.selectionEnd === inpAct.value.length) && (index + 1 <= 9) && (this.inputs.length === index + 1)) {
                const newId = this.inputs.length + 1;
                const newInput = {
                    id: newId,
                    value: ''
                };
                this.inputs.splice(index + 1, 0, newInput);
                this.$nextTick(() => {
                    this.$refs.inputRefs[index + 1].focus();
                });
            }
        },
        //Borra inputs
        deleteInput(index) {
            //Si la cantidad de inputs es mayor a dos
            if (this.inputs.length > 2) {
                
                if (index === this.inputs.length - 1 && this.inputs[index].value === '') {
                    this.inputs.splice(index, 1);
                    this.$refs.inputRefs[index - 1].focus();
                } else if (index !== 0 && this.inputs[index].value === '') {
                    this.inputs.splice(index, 1);
                    this.$refs.inputRefs[index - 1].focus();
                }
            }
        },
        onKeyUp(index,event){
            const {target, code} = event
            const {selectionStart} = target
            //Si presiona flecha izq y el input no es 0 y la pos del texto es 0
            if(code === "ArrowLeft" && index!==0 && selectionStart === 0){
                if(selectionStart === this.delayI){
                    const inpAnt = this.$refs.inputRefs[index - 1]//referente a un input anterior
                    const end = inpAnt.value.length//largo del contenido del input anterior
                    inpAnt.focus();//Se enfoca en el input anterior
                    inpAnt.setSelectionRange(end, end, "forward")// Se posiciona al final del contenido del input anterior
                    this.delayI--
                }else{this.delayI++}
            }
            
        },
        onKeyDown(index,event){
            const {code} = event
            //Si presiona flecha der y el input no es el ultimo
            if(code === "ArrowRight" && index !== this.inputs.length){
                const inpAct = this.$refs.inputRefs[index]//referente al input actual
                //Si existe un input a la derecha y si la pos del input actual es la final
                if((index + 1 < this.inputs.length) && (inpAct.value.length === inpAct.selectionEnd)){
                    this.$refs.inputRefs[index + 1].focus(); //Se enfoca en el proximo input
                }
            }
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