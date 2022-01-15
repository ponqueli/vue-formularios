<template>
    <div>
        <label 
            :class="inputClassesLabel">{{ customLabel }}
        </label>
        <input 
            type="range"
            v-bind="$attrs" 
            :value="nomeVarialEuEscolhi"
            :class="inputClassesInput"
            id="customRange1"
            @change="atualizar">
    </div>
</template>

<script>

export default {
    inheritAttrs: false,
    model:{
        prop: 'nomeVarialEuEscolhi', //padrao é value
        event: 'change'
    },
    props:{
        label: String,
        nomeVarialEuEscolhi: [Number, String],
        inputClassesInput: [String, Object, Array],
        inputClassesLabel: [String, Object, Array]
    },
    computed:{
        customLabel(){
            return `${this.label} (R$ ${ this.nomeVarialEuEscolhi || this.$attrs.min })`
        }
    },
    methods:{
        atualizar(event){
            const valor = event.target.value
            this.$emit('change', valor)
        }
    },
    created(){
        console.log('Attrs: ', this.$attrs)
    }
}
</script>