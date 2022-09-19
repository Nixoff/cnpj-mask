<script lang="ts">
import { defineComponent, onMounted, ref } from "vue";
import api from "../services/api";


export default {
    data() {
        return {
            teste: 'dasdasdsa'
        }
    },
    methods:{
        formatCnpj(cnpj: any) {
            if (cnpj === 0) return "";
            let formatedCnpj = cnpj.toString();
            let cnpjRegEx = /^(\d{2})(\d{3})(\d{3})(\d{4})(\d{2})/
            let validatedCnpj = formatedCnpj.replace(cnpjRegEx, "$1.$2.$3/$4-$5");
            return validatedCnpj
        }
    },
    name: "Home",
    setup() {
        const cnpj = ref([]);
        const fetchCnpj = async () => api.get("/empresas").then((res) => {
            cnpj.value = res.data;
            // cnpjValidator(cnpj.value);
             
        })

        onMounted(fetchCnpj); // LifeCycle quando monta o componente - chama a função da linha 15

        // function cnpjValidator(cnpjs: any) {
        //     cnpjs.map((x: any) => formatCnpj(x.cnpj))
        // }

        // function formatCnpj(cnpj: any) {
        //     if (cnpj === 0) return "";
        //     let formatedCnpj = cnpj.toString();
        //     let cnpjRegEx = /^(\d{2})(\d{3})(\d{3})(\d{4})(\d{2})/
        //     let validatedCnpj = formatedCnpj.replace(cnpjRegEx, "$1.$2.$3/$4-$5");
        //     return validatedCnpj
        // }
    }
}




</script>
    
<template>

    <p>{{ cnpj }}</p>
    <!-- <div v-for="cnpj in validatedCnpjList" :key="cnpj.cnpj"> -->
    <!-- <div v-for="cnpj in validatedCnpjList">
        <ul>
          <li>{{ cnpj.cnpj }}</li>
        </ul>
      </div> -->

    <!-- <button @click="logger()">Teste</button> -->
</template>
    
<style scoped>
.read-the-docs {
    color: #888;
}

* {
    outline: none !important;
}
</style>
    