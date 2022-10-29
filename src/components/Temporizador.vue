<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempoEmSegundos="tempoEmSegundos" />
        <Botao icone="fas fa-play" texto="play" @aoClicar="iniciar" :enabled="!tarefaIniciada || tarefaPausada" />
        <Botao icone="fas fa-pause" texto="pause" @aoClicar="pausar" :enabled="tarefaIniciada && !tarefaPausada" />
        <Botao icone="fas fa-stop" texto="stop" @aoClicar="finalizar" :enabled="tarefaIniciada" />
    </div>
</template>

<script lang="ts">
    import { defineComponent } from 'vue';
    import Cronometro from './Cronometro.vue';
    import Botao from './Botao.vue'
    export default defineComponent({
        name: 'TaskTemporizador',
        emits: ['aoTemporizadorFinalizado'],
        components:{
            Cronometro,
            Botao
        },
        data(){
            return{
                tempoEmSegundos: 0,
                cronometro: 0,
                tarefaIniciada: false,
                tarefaPausada: false
            }
        },
        methods:{
            iniciar(){
                this.cronometro = setInterval(() => {
                    this.tempoEmSegundos += 1;
                }, 1000);
                this.tarefaIniciada = true;
                this.tarefaPausada = false;
            },
            pausar(){
                clearInterval(this.cronometro);
                this.tarefaPausada = true;
            },
            finalizar(){
                clearInterval(this.cronometro);
                this.tarefaIniciada = false;
                this.tarefaPausada = false;
                this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos);
                this.tempoEmSegundos = 0;
            }
        }
    })
</script>