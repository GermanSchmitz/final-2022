<template>
    <section class="src-components-conversor-pesos-dolares">
        <h1>Conversor a dólares</h1>
        <label for="inputPesos">Ingrese un monto $</label>
        <input
            type="number"
            name="inputPesos"
            id="inputPesos"
            v-model="cantidadPesos"
        />
        <br />
        <br />
        <label for="inputDolares">Valor del dólar en $</label>
        <input
            type="number"
            name="inputDolares"
            id="inputDolares"
            v-model="precioDolar"
        />
        <label for="checkBoxUpdate">- Actualización</label>
        <input
            type="checkbox"
            name="checkBoxUpdate"
            id="checkBoxUpdate"
            v-model="inputCheckBox"
            @click="this.getPrecioDolarApi"
        />
        <span v-if="inputCheckBox">{{ this.traerFechaYHora }}</span>
        <p>Valor convertido USD {{ this.calcularCantidadDolares }}</p>
        <br />
        <br />
        <br />
        <br />
        <h2>Respuestas choice</h2>
        <p>
            1) c <br />
            2) b <br />
            3) c <br />
            4) a <br />
            5) b <br />
        </p>
    </section>
</template>

<script>
export default {
    name: "src-components-conversor-pesos-dolares",
    props: [],
    mounted() {},
    data() {
        return {
            precioDolar: undefined,
            cantidadPesos: undefined,
            inputCheckBox: false,
            urlApi: "https://www.dolarsi.com/api/api.php?type=valoresprincipales",
            arrApi: [],
        };
    },
    methods: {
        async getPrecioDolarApi() {
            try {
                const respuesta = await this.axios(this.urlApi);
                this.precioDolar = parseInt(respuesta.data[1].casa.compra);
                console.log(this.precioDolar);
            } catch (e) {
                console.log(e);
            }
        },        
    },
    computed: {
        calcularCantidadDolares() {
            let cantidad = this.cantidadPesos / this.precioDolar;
            return cantidad > 0 ? cantidad : 0;
        },
        traerFechaYHora() {
            return new Date().toLocaleString();
        }
    },
};
</script>

<style scoped lang="css"></style>
