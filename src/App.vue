<template>
    <div id="app">
        <h1>Lista de Presentes</h1>
        <div class="presente-lista">
            <PresenteItem
                v-for="presente in presentesOrdenados"
                :key="presente.id"
                :presente="presente"
                @comprar="marcarComoComprado"
            />
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
                    nome: "Conjunto de facas",
                    imagem: "https://m.media-amazon.com/images/I/518Y9L-71uL._AC_SL1000_.jpg",
                    link: "https://www.amazon.com.br/Facas-Pe%C3%A7as-Plenus-Tramontina-Cutelaria/dp/B07K32CH6K/",
                    comprado: false,
                },
                {
                    id: 1,
                    nome: "Taboa de corte",
                    imagem: "https://m.media-amazon.com/images/I/61O-LE1wxpL._AC_SL1200_.jpg",
                    link: "https://www.amazon.com.br/Estampa-Legumes-Vegetais-Frutas-M%C3%A1rmore/dp/B0D9GFC4H4/ref=sr_1_17_sspa?__mk_pt_BR=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dib=eyJ2IjoiMSJ9.fNt92Ztz4SdWwl5NJvI53FuXhbGRyZvHxMXZW3a6ncsoknmIHAxaDdp6v3KzaE79YCZR0WT5hV6WVYz8qSeHI4l8V7tkFbBZXkzQ-D7nyC-PTyocZ6_SY9FM5Q_zL1aWQplUkR8dhvoQ0xZ6a8UoTQ.lpqK_q0pqw6GNzmPbTenPb7KTayu9w-y3_aKg7YrWBQ&dib_tag=se&keywords=tabua%2Bde%2Bcorte%2Bde%2Bplastico&qid=1727827933&s=kitchen&sr=1-17-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGZfbmV4dA&th=1",
                    comprado: false,
                },
                {
                    id: 1,
                    nome: "Afiador de facas",
                    imagem: "https://m.media-amazon.com/images/I/51RxZHBYZsL._AC_SL1200_.jpg",
                    link: "https://www.amazon.com.br/Afiador-Amolador-Diamantado-est%C3%A1gios-ergon%C3%B4mico/dp/B0CFGC22LR/ref=sr_1_13?__mk_pt_BR=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=3I9MRKSGHB4SG&dib=eyJ2IjoiMSJ9.iJcUuO-0LOm6AGv7VtepK5uqzVd6Z7uScLwGQQpC43Q6wwd_nUR7_YxNTqjJopuc1r-CrFDvaJuyntRdSdOBb_ZwHGgvSA7oP6n2Q2cykEW3Ik-5wfrwPtVfnQgnxUT60iWprbUmIxytREBnOt5qODQuJmz771_KzCALBkba88uFD7dBJD525pW_tVKATnqCS0R-EDIYv0YC0q1weU1nYyCoI9Rdvr7YxBi2P9lIiro.hs1Afho0gfZr0B6yaXeYq478xIPd453y7cCMpxU2UE0&dib_tag=se&keywords=afiador+de+facas+preto&qid=1727828382&s=kitchen&sprefix=afiador+de+facas+preto%2Ckitchen%2C216&sr=1-13",
                    comprado: false,
                },
                {
                    id: 1,
                    nome: "Conjunto Utensílios de Silicone",
                    imagem: "https://m.media-amazon.com/images/I/51+7N6sPtqL._AC_SL1000_.jpg",
                    link: "https://www.amazon.com.br/Conjunto-Utens%C3%ADlios-Cozinha-Pe%C3%A7as-Silicone/dp/B07W3XTM9Y/ref=sr_1_5?__mk_pt_BR=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=3OKVXAI8MWE9P&dib=eyJ2IjoiMSJ9.RpzYFn0OqbZXLQ3dLXUPEJxEu6J-tQwKBcAaFqB5jaNoabWdhMF7WuhBTrzpOIx0Cj4DPaykHY4T_eWuSCdWS3FNbNN4enZE8nnXIbrXAbkbR0bD-xaHnZKSBqJFfESATfEXjKZh_9SD3WgP4AJ1MrworPkvcaKpQZRGwSphIyrErOpJG-Kx1w1y_gSRnZoiMRW5T1Hn3YmrNLvtww8sisqbTTUEvS6SkZ5DD-BygxE.Jdqhyfyd-2l1yrHOky0ZX--vTXzrg137eyNN5GABFCI&dib_tag=se&keywords=conjunto+de+utens%C3%ADlios+de+silicone&qid=1727828553&s=kitchen&sprefix=conjunto+de+utens%C3%ADlios+de+silicone%2Ckitchen%2C223&sr=1-5",
                    comprado: false,
                },
                {
                    id: 1,
                    nome: "Ralador queijo/legumes de inox",
                    imagem: "https://www.amazon.com.br/Ralador-Pratic-Brinox-2204-328/dp/B08KLW44S7/ref=sr_1_4?crid=3V5FBPIF56BY6&dib=eyJ2IjoiMSJ9.qqW6UPIOWDG1IgHNoAnDQAieqtc8eTYBbMM2FpPF5wsR5v8VHiQY_031fZpGsRid_sRxLdRyxT7eKpG5b83MYS6GXj95e6QvNWfu_jAi0bJXMWjLLNS3Bv79REOPKR8zqwFEHJf0utZEJNU7u1slrVMbnvfV5_abnUOak3PponvYRxib9AESWiSBBXuGE4co5oJ_mRLp44G1EERU8yUx2R18boMyrGm1v9TZRo1TJtzE8mgmczXj1UcRDLSuqRUyicKDnhqJNapN03MiXYhmIbuBJUN3O8T3B38ngp8zKYw.PCiH1aVDDA5yox9Vsx3So2YCTLdJBpJTHkvynfgFHCk&dib_tag=se&keywords=ralador+inox+6+faces&qid=1727828847&sprefix=ralador+inox+6+fa%2Caps%2C227&sr=8-4",
                    link: "https://m.media-amazon.com/images/I/519hOQj-RkL._AC_SL1000_.jpg",
                    comprado: false,
                },
                {
                    id: 1,
                    nome: "Descascador de legumes",
                    imagem: "https://www.amazon.com.br/Mundial-Descascador-cer%C3%A2mico-FC05-D/dp/B07BBT5CZ2/ref=sr_1_15?crid=7L0L0FQW6IEJ&dib=eyJ2IjoiMSJ9.hFEcYWeWJx_ywy5m13zIRuo_-3UIY5SDrcJ1jPvwCAnZ92aaj8dQamT89sA7_tsZhjbLDA0e9GRyg6YlwkeY6G0I78tzna9PX5DK6WxO0PGaQQyFvk6KGYtu9XmVh766xEsLlj2KTsxfPOyH0Huim9TuDb3RxvzGAeUPkKeRBBqpZA4zo1Yq7dOk9JoEgEgqu38vLhHG5OZwrqYesr4VIPrrVvaeOqxi2-dk6Jta6I1KpIJryun9tIssJRtg6Ar8-B8hiCVrA8yy4092kLaUnd_1RKRaQ_Yp8JjElULhlng.pkJKQh6WNoTo3iy3LzrrCExgc4sYbYRipbHfshrqwZQ&dib_tag=se&keywords=descascador+de+legumes&qid=1727828939&sprefix=desca%2Caps%2C236&sr=8-15",
                    link: "https://m.media-amazon.com/images/I/51ZJUDSrFqL._AC_SL1000_.jpg",
                    comprado: false,
                },
                {
                    id: 1,
                    nome: "Abridor de latas",
                    imagem: "https://www.amazon.com.br/Abridor-Latas-Manivela-Profissional-Pl%C3%A1stico/dp/B0D1D9YX81/ref=sr_1_18?crid=195OUN0KFCW6&dib=eyJ2IjoiMSJ9.LChMxNn339dlXZMlkVF4IPUnlYqEoP68puZLD-FPRdaQpQ4PP1zyqxyxrQdTIOwdHWJC_FMZdp2rMp39fIYrfJpsdhgAYzmeb1vNlagmoD2aZkGKVh_rfMI7oALojznGaPi1Y1-R8aIW2iBZGf3r1osQcY9R0r7v5o17tcbL4-CTBxuW5SWt66r3HibzcQ5SCFa87eOLIcJcbdjXuUsfUSWpyXpkyj-fdYuDIri_Y8jM5kONjnQ8Qe6NZhrHzSr-A0T5bgp783STZru8rHyAknk6JVs9NbiG-OuBG7qx8X8.ySi1SautCMXvGlrlyCu2wtLkjRSRWqsAKYuwtXRAl_c&dib_tag=se&keywords=abridor+de+latas&qid=1727829091&sprefix=abridor%2Caps%2C236&sr=8-18",
                    link: "https://m.media-amazon.com/images/I/71Ne8K26ATL._AC_SL1500_.jpg",
                    comprado: false,
                },
                {
                    id: 1,
                    nome: "Conjunto de medidores",
                    imagem: "https://m.media-amazon.com/images/I/61fRCpwp1kL._AC_SL1200_.jpg",
                    link: "https://www.amazon.com.br/Medidores-Cozinha-Colheres-Medidor-Culin%C3%A1rio/dp/B0CSVRSCGC/ref=sr_1_57_sspa?__mk_pt_BR=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=18RAZMQVPEZ1X&dib=eyJ2IjoiMSJ9.w6Oh5zyc6bGvmziRCVZEf9aGl7s0eaNvaOVqY6-9WS_yIBxsaj_Jdxz6yy4dbaHVR8uUQjzHkivGIh2C8qv1V6zHT-Fj_iYW8YHt1T5bQsQA0ZVj_nvdiSFywgM2t_qZUtv_t2P26gvjlqPs0UIA4q-u_3D65xXcRJBdle1idBcFIMezBi-2uAW78QJhuaRPcuf4DtcyWrQcRYQ14b3n4goi4OoIywaPj4NVb63J1Uk0r7xr868HyU7UluG8xIRenjnPYozJPognnPDjebUIk2RfD1tBMbjKpERz5iUw7Sk.ZEF7EM5YY0tZejFSdgiS4-mmVwuAj5SNyOng2-NaUBc&dib_tag=se&keywords=Conjunto%2Bde%2Bmedidores%2Bde%2Bcozinha&qid=1727829312&sprefix=conjunto%2Bde%2Bmedidores%2Bde%2Bcozinha%2Caps%2C251&sr=8-57-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9idGY&th=1",
                    comprado: false,
                },
                {
                    id: 1,
                    nome: "Kit de peneiras",
                    imagem: "https://m.media-amazon.com/images/I/61nbhl4GxmL._AC_SL1154_.jpg",
                    link: "https://www.amazon.com.br/Jogo-Peneiras-Conjunto-Resistente-Inox/dp/B0D35Z9HTT/ref=sr_1_2_sspa?__mk_pt_BR=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=1D5MCRR99VWKT&dib=eyJ2IjoiMSJ9.u9mKuY2eyHgUllKPRkSukuaRF6TB1h7l3OGYo_q8QTc8zk2gyDBg1KVjVvSgfojazp9FY4dlrM50a2N2ljPJSRHNMDSIAiyHtaqaYzlUPTWNF2y3C2K_OdphOLSYPVHZ2es-fO8JDier9lQv355Cz0OSW0jZIiAhSWrkT7SFJePHlwpPzskAUt5BQZ21W0n-n_URJXzFk_WXRFuOYfvDLaM8QMEVtdLkwfDg9MCkYx5_54WiJ1UEqXWbShkp6Qw2Xfwku9AylbX-IiKzOFmM-Pyo27Cl2q9P0m7ZRmH6oOA.njgNQkvg4zOQwQ82YYZ3yRxYGgvugGWycFsV1kcFDC4&dib_tag=se&keywords=conjunto+de+peneira&qid=1727829484&sprefix=conjunto+de+peneira%2Caps%2C389&sr=8-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1",
                    comprado: false,
                },
            ],
        };
    },
    computed: {
        presentesOrdenados() {
            return [...this.presentes].sort((a, b) => a.comprado - b.comprado);
        },
    },
    methods: {
        marcarComoComprado(id) {
            const presente = this.presentes.find((p) => p.id === id);
            if (presente) presente.comprado = true;
        },
    },
};
</script>

<style scoped>
#app {
    text-align: center;
    padding: 20px;
}

.presente-lista {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    gap: 20px;
}

h1 {
    font-size: 32px;
    color: #556b2f; /* Verde oliva */
    margin-bottom: 40px;
}

@media (max-width: 768px) {
    .presente-lista {
        flex-direction: column;
        align-items: center;
    }
}
</style>
