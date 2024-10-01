<template>
    <div id="app">
        <h1>Lista de Presentes</h1>
        <div v-for="presente in presentesOrdenados" :key="presente.id">
            <PresenteItem :presente="presente" @comprar="marcarComoComprado" />
        </div>
    </div>
</template>

<script>
import PresenteItem from "./components/PresenteItem.vue";

export default {
    components: {
        PresenteItem,
    },
    data() {
        return {
            presentes: [
                {
                    id: 1,
                    nome: "Liquidificador",
                    imagem: "https://m.media-amazon.com/images/I/518Y9L-71uL._AC_SL1000_.jpg",
                    link: "https://www.amazon.com.br/Facas-Pe%C3%A7as-Plenus-Tramontina-Cutelaria/dp/B07K32CH6K/ref=sr_1_5?c=ts&dib=eyJ2IjoiMSJ9.a3VhWs63Tw4eUYWmmc8uYwHTfj93ZlXiGNYGLLfSdhxnFSDkBu60ClMXOqebqAFbeS4S6KwIr5axWOs5ih09MUUEgbzqirzm004nSTnYaYtvfrMiFm2BBuyopN4oJLCOLRNjQsqUomIdVqgnJxTMESlpBeNMjrZ-SNEeGvjC1fYtW63sGrxoRpY4IdE7r3EoorAhN9-7B-RQrZPVDbnTEqE12qQNPyhCSZ4pgYKd87c.cABDQT3ovAVNIcJZC_dweJyvcYUYfPVqXuMEX8hmHQ0&dib_tag=se&keywords=Facas+de+Cozinha+e+Acess%C3%B3rios&qid=1727819131&s=kitchen&sr=1-5&ts_id=17124819011",
                    comprado: false,
                },
                {
                    id: 2,
                    nome: "Torradeira",
                    imagem: "link_da_imagem",
                    link: "link_para_compra",
                    comprado: false,
                },
                // Adicione mais presentes aqui
            ],
        };
    },
    computed: {
        presentesOrdenados() {
            return this.getPresentesOrdenados();
        },
    },
    methods: {
        getPresentesOrdenados() {
            // Retorna uma cópia da lista ordenada
            return [...this.presentes].sort((a, b) => a.comprado - b.comprado);
        },
        marcarComoComprado(id) {
            const presente = this.presentes.find((p) => p.id === id);
            if (presente) presente.comprado = true;
        },
    },
};
</script>
