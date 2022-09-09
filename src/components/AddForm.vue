<template>
<div class="card p-4 mt-2 mb-4">
    <h2>Tambah Barang</h2>
    <div class="alert alert-danger m-0 py-2 hidden">
        Maaf ID yang anda masukan sudah ada!<img class="float-end m-0" @click="close" width="30" height="30" id="x" src="../../src/assets/close.png">
    </div>
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
            a: localStorage.getItem("barang") === "" ? [] : JSON.parse(localStorage.getItem("barang")),
            idbarang: [],
        }
    },
    methods: {
        submit() {
            function isEmpty(val) {
                return (val === undefined || val == null || val.length <= 0) ? true : false;
            }

            this.idbarang = this.a.filter((an) => {
                return an.id === this.barang.id;
            })

            if (isEmpty(this.idbarang) == false) {
                let errmsg = document.querySelector(".alert");
                errmsg.classList.remove("hidden")
            }
            if (isEmpty(this.idbarang) == true) {
                this.a.push(this.barang);
                localStorage.setItem("barang", JSON.stringify(this.a));
                this.barang = {
                    id: "",
                    namaBarang: "",
                    warnaBarang: "",
                    jumlahBarang: ""
                }
                location.reload()
            }
        },
        hide() {
            let modal = document.querySelector("#collapseExample");
            modal.classList.add("collapse");
        },
        close(){
            let errmsg = document.querySelector(".alert");
            errmsg.classList.add("hidden")
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
    margin-top: 10px;
}
.hidden {
    display: none;
}
#x{
    cursor: pointer;
}
.alert{
    border-left: 5px solid red;
}
.footer {

}
</style>
