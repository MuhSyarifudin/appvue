<template>
<div class="container">
    <h1>Daftar Barang</h1>
    <!--<div class="alert alert-success">
    Berhasil menambahkan {{ item.namaBarang }}!
    </div>-->
    <button class="btn btn-dark btn-tambah" type="button" data-toggle="collapse" data-target="#collapseExample" aria-expanded="false" aria-controls="collapseExample" @click="show">
        + Barang
    </button>
    <FormTable />
    <div class="collapse" id="collapseExample">
        <AddForm />
    </div>
</div>
</template>

<script>
import FormTable from "./components/FormTable.vue"
import AddForm from "./components/AddForm.vue"

export default {
    name: 'App',
    components: {
        FormTable,
        AddForm
    },
    mounted() {
        if (typeof (Storage) == undefined) {
            console.log("Maaf browser anda tidak mendukung localStorage!");
        } else {
            if (localStorage.getItem("barang") == null) localStorage.setItem("barang", []);
        }
    },
    methods: {
        show() {
            let modal = document.querySelector("#collapseExample");
            modal.classList.remove("collapse");
        }
    }
}
</script>

<style>
.btn-tambah {
    margin-left: 3px;
    margin-top: 15px;
    margin-bottom: 10px;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: left;
    color: #2c3e50;
    margin-top: 20px;
}
</style>
