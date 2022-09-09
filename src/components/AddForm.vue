<template>
<div class="container col-lg-8 mt-2 card p-3">
    <h2>Tambah Barang</h2>
    <form @submit.prevent="submit">
        <div class="form-group">
            <label for="name" class="float-start">ID Barang</label>
            <input type="number" class="form-control" v-model="barang.id" placeholder="Masukan id barang">
        </div>
        <div class="form-group">
            <label for="name" class="float-start">Nama Barang</label>
            <input type="text" class="form-control" v-model="barang.namaBarang" placeholder="Masukan nama barang">
        </div>
        <div class="form-group">
            <label for="email" class="float-start">Warna Barang</label>
            <input type="text" class="form-control" v-model="barang.warnaBarang" placeholder="Masukan warna barang">
        </div>
        <div class="form-group">
            <label for="address" class="float-start">Jumlah Barang</label>
            <input type="number" class="form-control" v-model="barang.jumlahBarang" placeholder="Masukan jumlah barang" />
        </div>
        <button type="submit" class="btn btn-primary mt-3">Submit</button>
        <button class="btn btn-danger mt-3" type="button" data-toggle="collapse" data-target="#collapseExample" @click="hide">
            Cancel
        </button>
    </form>
</div>
</template>

<script>
export default {
    name: "AddForm",
    data() {
        return {
            barang: {
                id: "",
                namaBarang: "",
                warnaBarang: "",
                jumlahBarang: ""
            },
            a: localStorage.getItem("barang") === "" ? [] : JSON.parse(localStorage.getItem("barang"))
        }
    },
    methods: {
        submit() {
            this.a.push(this.barang);
            localStorage.setItem("barang", JSON.stringify(this.a));
            this.barang = {
                id:"",
                namaBarang:"",
                warnaBarang:"",
                jumlahBarang:""
            }
            location.reload()
        },
        hide() {
            let modal = document.querySelector("#collapseExample");
            modal.classList.add("collapse");
        }
    },
}
</script>

<style scoped>
.btn-danger {
    margin-right: -700px;
    margin-left: 10px;
}

.form-group {
    margin-top: 10px
}
</style>
