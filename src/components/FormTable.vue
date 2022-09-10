<template>
<div class="card p-2">
    <table class="table table-striped table-bordered">
        <thead>
            <tr class="text-center table-dark">
                <th>No.</th>
                <th>ID</th>
                <th>Nama Barang</th>
                <th>Warna Barang</th>
                <th>Jumlah Barang</th>
                <th>Opsi</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for=" ( value , index ) in a " :key="value">
                <template v-if="idBarang === value.id">
                    <td class="font-weight-bold">{{ index + 1 }}.</td>
                    <td>
                        {{ value.id }}
                    </td>
                    <td>
                        <div>
                            <input for="nama" type="text" v-model="value.namaBarang" class="form-control-sm" />
                        </div>
                    </td>
                    <td>
                        <div>
                            <input id="warna" type="text" v-model="value.warnaBarang" class="form-control-sm" />
                        </div>
                    </td>
                    <td>
                        <div>
                            <input name="jumlah" type="number" v-model="value.jumlahBarang" class="form-control-sm" />
                        </div>
                    </td>
                    <td class="text-center">
                        <button @click="saveEdit(value)" class="btn btn-sm btn-success">Save</button>
                        <button @click="cancelEdit(value)" class="btn btn-sm btn-danger">Cancel</button>
                    </td>
                </template>
                <template v-else>
                    <td class="text-center">{{ index + 1 }}.</td>
                    <td class="text-center">{{ "B"+value.id }}</td>
                    <td class="text-center text-capitalize text-wrap">{{ value.namaBarang }}</td>
                    <td class="text-center text-capitalize">{{ value.warnaBarang }}</td>
                    <td class="text-center">{{ value.jumlahBarang }}</td>
                    <td class="text-center">
                        <button class="btn btn-warning btn-sm" @click="editBarang(value)">Edit</button>
                        <button class="btn btn-danger btn-sm" @click="deleteBarang(value.id)">Delete</button>
                    </td>
                </template>
            </tr>
        </tbody>
    </table>
</div>
</template>

<script>
export default {
    name: 'FormTable',
    props: {
        msg: String
    },
    data() {
        return {
            idBarang: null,
            a: localStorage.getItem("barang") === "" ? [] : JSON.parse(localStorage.getItem("barang")),
            data: ""
        }
    },
    methods: {
        deleteBarang(id) {
            this.a = this.a.filter((an) => {
                return an.id !== id;
            })
            localStorage.setItem("barang", JSON.stringify(this.a));
        },
        editBarang(barang) {
            this.data = Object.assign({}, barang);
            this.idBarang = barang.id;
        },
        saveEdit(value) {
            let id = this.data.id;
            this.a = this.a.map((an) => {
                return an.id === id ? value : an
            });
            localStorage.setItem("barang", JSON.stringify(this.a))
            this.idBarang = null;
        },
        cancelEdit(value) {
            Object.assign(value, this.data);
            this.idBarang = null;
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style scoped>
button {
    margin-right: 10px;
}

.btn-tambah {
    margin-left: -800px;
}

thead,
tbody {
    width: 100%;
}
</style>
