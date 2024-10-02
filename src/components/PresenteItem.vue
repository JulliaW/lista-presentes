<template>
    <div
        class="card"
        :class="{ comprado: presente.comprado }"
        :style="{ opacity: presente.comprado ? 0.5 : 1 }"
    >
        <img :src="presente.imagem" @click="abrirLink(presente.link)" class="imagem-card" />
        <p class="titulo">{{ presente.nome }}</p>
        <button @click="marcarComoComprado" :disabled="presente.comprado" class="comprado-botao">
            {{ presente.comprado ? "Já foi presenteado" : "Comprei para presentear" }}
        </button>
    </div>
</template>

<script>
export default {
    props: ["presente"],
    methods: {
        abrirLink(link) {
            window.open(link, "_blank");
        },
        marcarComoComprado() {
            this.$emit("comprar", this.presente.id);
        },
    },
};
</script>

<style scoped>
.card {
    background-color: #fff;
    border: 2px solid #556b2f; /* Verde oliva */
    border-radius: 15px;
    padding: 20px;
    transition: transform 0.3s;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    max-width: 250px;
    margin: 10px auto;
}

.card:hover {
    transform: scale(1.05);
}

.card.comprado {
    opacity: 0.6; /* Efeito visual para os comprados */
}

.imagem-card {
    width: 100%;
    height: auto;
    border-radius: 10px;
    cursor: pointer;
    margin-bottom: 15px;
}

.titulo {
    font-size: 18px;
    color: #556b2f; /* Verde oliva */
    margin-bottom: 10px;
}

.comprado-botao {
    background-color: #556b2f; /* Verde oliva */
    color: white;
    border: none;
    padding: 10px 15px;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.3s;
}

.comprado-botao:disabled {
    background-color: #a9a9a9; /* Cinza para botão desabilitado */
    cursor: not-allowed;
}

.comprado-botao:hover:not(:disabled) {
    background-color: #6b8e23; /* Tom mais claro de verde oliva */
}
</style>
