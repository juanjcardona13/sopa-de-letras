<template>
  <div id="app">
    <b-row class="m-5">
        <!--TITULO-->
        <b-col cols="12" class="align-c-c">
            <h4 class="text-primary">Sopa de letras</h4>
        </b-col>
        <!--ALTO-->
        <b-col cols="6" style="display: grid" class="align-r-c mt-3">
            <label for="alto"><b>Alto:</b></label>
            <b-input style="width: 100%" @change="FuncOrdenarPalabra()" min="12" max="20" v-model="alto" type="number" step="1" placeholder="Por favor indica el alto..." />
        </b-col>
        <!--ANCHO-->
        <b-col cols="6" style="display: grid" class="align-l-c mt-3">
            <label for="ancho"><b>Ancho:</b></label>
            <b-input style="width: 100%" @change="FuncOrdenarPalabra()" min="12" max="20" v-model="ancho" type="number" step="1" placeholder="Por favor indica el ancho..." />
        </b-col>
        <!--BOTON-->
        <b-col cols="12" class="align-c-c mt-5">
            <b-button variant="primary" style="width: 25%" @click="FuncOrdenarPalabra()">Revolver</b-button>
        </b-col>
        <!--SOPA DE LETRAS-->
        <b-col cols="8" class="align-r-c mt-4">
            <div class="card">
                <b-container>
                    <div id="puzzle-container"></div>
                </b-container>
            </div>
        </b-col>
        <!--PALABRAS-->
        <b-col cols="4" class="align-c-c mt-4">
            <div class="card">
                <b-container class="p-3">
                    <div id="puzzle-words" class="text-capitalize"></div>
                    <div class="m-3 align-c-c">
                        <input type="button" @click="FuncSolucionar()" class="btn btn-success" value="Resolver sopa de letras"/>
                    </div>
                </b-container>
            </div>
        </b-col>
    </b-row>
  </div>
</template>

<script>
import * as WordFindGame from './wordfind/wordfindgame.min.js'

export default {
    name: 'App',
    data() {
        return {
            alto: 12,
            ancho: 12,
            sopaDeLetras: null,
            abecedario: 'abcdefghijklmnopqrstuvwxyz',
            arrPalabras: [
                'águila',
                'ballena',
                'burro',
                'caballo',
                'canguro',
                'cebra',
                'cerdo',
                'cocodrilo',
                'elefante',
                'gallina',
                'gato',
                'hipopótamo',
                'jirafa',
                'león',
                'oso',
                'perro',
                'serpiente',
                'tigre',
                'tortuga',
                'vaca',
            ]
        }
    },
    mounted() {
        this.FuncOrdenarPalabra()
    },
    methods: {
        FuncOrdenarPalabra() {
            let palabras = this.arrPalabras;
            let opciones = {
                height: this.alto,
                width:  this.ancho,
                orientations: ['horizontal', 'vertical', 'diagonal'],
                fillBlanks: true,
            }
            this.sopaDeLetras = window.wordfindgame.create(palabras, '#puzzle-container', '#puzzle-words', opciones);
        },
        FuncSolucionar() {
            wordfindgame.solve(this.sopaDeLetras, this.arrPalabras);
        },
        FuncAleatorio() {
            return Math.floor((Math.random() * 10) + 1)
        }
    }
}
</script>

<style>
@import './assets/main.css';
@import './wordfind/wordfind.css';
</style>

