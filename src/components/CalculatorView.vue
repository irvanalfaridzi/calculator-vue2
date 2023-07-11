<template>
    <div id="calculator-view" class="w-auto h-screen bg-slate-800 grid grid-cols-4 gap-4 text-white p-4 text-4xl">
        <input v-model="display" class="col-span-4 text-slate-800 text-right text-7xl" type="number" name="input" id="input">
        <button v-on:click="calculate('AC')" class="col-auto bg-slate-700">AC</button>
        <button v-on:click="calculate('-+')" class="bg-slate-700">+/-</button>
        <button v-on:click="calculate('%')" class="bg-slate-700">%</button>
        <button v-on:click="calculate('/')" class="bg-yellow-500">/</button>
        <button v-on:click="numberButton(7)" class="bg-slate-600">7</button>
        <button v-on:click="numberButton(8)" class="bg-slate-600">8</button>
        <button v-on:click="numberButton(9)" class="bg-slate-600">9</button>
        <button v-on:click="calculate('x')" class="bg-yellow-500">x</button>
        <button v-on:click="numberButton(4)" class="bg-slate-600">4</button>
        <button v-on:click="numberButton(5)" class="bg-slate-600">5</button>
        <button v-on:click="numberButton(6)" class="bg-slate-600">6</button>
        <button v-on:click="calculate('-')" class="bg-yellow-500">-</button>
        <button v-on:click="numberButton(1)" class="bg-slate-600">1</button>
        <button v-on:click="numberButton(2)" class="bg-slate-600">2</button>
        <button v-on:click="numberButton(3)" class="bg-slate-600">3</button>
        <button v-on:click="calculate('+')" class="bg-yellow-500">+</button>
        <button v-on:click="numberButton(0)" class="col-span-2 bg-slate-600">0</button>
        <button class="bg-slate-600">,</button>
        <button v-on:click="equal" class="bg-yellow-500">=</button>
    </div>
</template>

<script>
export default {
    name: 'CalculatorView',
    data(){
        return{
            input: 0,
            input2: 0,
            action: null,
            display: 0,
            isPressed : false,
        }
    },
    methods: {
        numberButton(x){
            if (this.input == 0) {
                this.input = x;
                this.display = this.input;
                return;
            }
            this.input = this.input.toString().concat(x.toString());
            this.display = this.input;
        },
        calculate(x){
            if (this.action == x && this.isPressed) {
                return;
            }

            if (this.action == '/') {
                this.display = this.input2 / this.input;
            } else  if (this.action == 'x') {
                this.display = this.input2 * this.input; 
            } else if (this.action == '-') {
                this.display = this.input2 - this.input;
            }  else if (this.action == '+') {
                this.display = this.input2 + this.input;
            } else if (x == '-+'){
                this.display *= -1;
                return;
            } else if(x == '%'){
                this.display /= 100;
                return;
            } else if (x == 'AC'){
                this.input = 0;
                this.input2 = 0;
                this.action = null;
                this.display = this.input;
                return;
            }

            this.input = this.display; 
            this.input2 = this.input;
            this.input = 0;
            this.action = x;
        },
        equal(){
            this.calculate(this.action);
            this.action = null;
        }
    }
}
</script>