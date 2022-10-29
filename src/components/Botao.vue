<template>
    <button class="button" @click="click" :disabled="!enabled">
        <span class="icon">
            <i :class="icone"></i>
        </span>
        <span>{{texto}}</span>
    </button>
</template>

<script lang="ts">
    import { defineComponent } from 'vue';
    export default defineComponent({
        name: 'TemporizadorBotao',
        emits: ['aoClicar'],
        props:{
            texto:{
                type: String,
                default: ''
            },
            icone:{
                type: String,
                default:'fas'
            },
            enabled:{
                type: Boolean,
                default: true
            }
        },
        methods:{
            click(){
                this.$emit('aoClicar');
            }
        }
    })
</script>