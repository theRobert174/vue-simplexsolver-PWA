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
                @keydown.enter="addInput(index + 1)"
                @keydown.right="addInput(index + 1)"
                @keydown.backspace="deleteInput(index)"
                ref="inputRefs"
                :style="{ 'min-width': '5px', 'width': input.width + 'px' }"
            />
            <label :for="'input-' + input.id">x<sub>{{ input.id }}</sub></label>
        </div>
    </div>
</template>

<script>
export default {
    name: "FormEquation",
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
            if ((this.inputs[index - 1].value !== '') && (index <= 9) && (this.inputs.length === index)) {
                console.log(this.inputs.length, index)
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
        },
        deleteInput(index) {
            if (this.inputs.length > 2) {
                if (index === this.inputs.length - 1 && this.inputs[index].value === '' && event.keyCode === 8) {
                    this.inputs.splice(index, 1);
                    this.$refs.inputRefs[index - 1].focus();
                } else if (index !== 0 && this.inputs[index].value === '' && event.keyCode === 8) {
                    this.inputs.splice(index, 1);
                    this.$refs.inputRefs[index - 1].focus();
                }
            }
        },
        /*navigateInputs(direction, index) {
            if (direction === 'right' && this.inputs[index].value === '') {
                if (index === this.inputs.length - 1) {
                    this.addInput(index + 1);
                } else {
                    this.$refs.inputRefs[index + 1].focus();
                }
            } else if (direction === 'left' && this.inputs[index].value === '') {
                if (index !== 0) {
                    this.$refs.inputRefs[index - 1].focus();
                    this.deleteInput(index);
                }
            }
        }*/
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