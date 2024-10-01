<template>
    <div class="presente-lista">
        <PresenteItem
            v-for="presente in presentesOrdenados"
            :key="presente.id"
            :presente="presente"
            @comprar="marcarComoComprado"
        />
    </div>
</template>

<script>
import PresenteItem from "./components/PresenteItem.vue";

export default {
    components: {
        PresenteItem,
    },
    props: {
        presentes: Array,
    },
    computed: {
        presentesOrdenados() {
            return [...this.presentes].sort((a, b) => a.comprado - b.comprado);
        },
    },
    methods: {
        marcarComoComprado(id) {
            this.$emit("comprar", id);
        },
    },
};
</script>

<style scoped>
.presente-lista {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    gap: 20px;
    padding: 20px;
}

@media (max-width: 768px) {
    .presente-lista {
        justify-content: center;
    }
}
</style>
