<script lang="ts">
import { ref, defineComponent } from 'vue'
import axios from 'axios'
import DefaultCard from '@/components/Forms/DefaultCard.vue'
import DefaultLayout from '@/layouts/DefaultLayout.vue'

export default defineComponent({
  name: 'FormPeminjaman',
  components: {
    DefaultLayout,
    DefaultCard
  },
  data() {
    return {
      inputNama: '',
      inputKeperluan: '',
      inputTanggalpinjam: '',
      inputTanggalkembali: '',
      inputAlat: '',
      inputNohp: '',
      inputStatus: ''
    }
  },
  methods: {
    async addPeminjaman() {
      try {
        const newPeminjaman = {
          nama: this.inputNama,
          keperluan: this.inputKeperluan,
          tanggalpinjam: this.inputTanggalpinjam,
          tanggalkembali: this.inputTanggalkembali,
          alat: this.inputAlat,
          nohp: this.inputNohp,
          status: this.inputStatus
        }

        const response = await axios.post('http://localhost:3000/peminjamans', newPeminjaman)

        console.log('Peminjaman added successfully:', response.data)

        // Clear form inputs after successful submission
        this.inputNama = ''
        this.inputKeperluan = ''
        this.inputTanggalpinjam = ''
        this.inputTanggalkembali = ''
        this.inputAlat = ''
        this.inputNohp = ''
        this.inputStatus = ''
        this.$router.push({ name: 'tables' })
      } catch (error) {
        console.error('Error adding peminjaman:', error)
        // Handle error here
      }
    }
  }
})
</script>

<template>
  <DefaultLayout>
    <!-- Breadcrumb Start -->
    <!-- <BreadcrumbDefault :pageTitle="pageTitle" /> -->
    <!-- Breadcrumb End -->

    <!-- ====== Form Layout Section Start -->
    <div class="">
      <div class="flex flex-col gap-9">
        <!-- Contact Form Start -->
        <DefaultCard cardTitle="Isi data dengan Benar">
          <div class="p-6.5">
            <div class="mb-5">
              <label class="mb-3 block text-black dark:text-white"> Nama Peminjam </label>
              <input
                type="text"
                v-model="inputNama"
                placeholder="Masukkan Nama"
                class="w-full rounded-lg border-[1.5px] text-black border-stroke bg-transparent py-3 px-5 font-normal outline-none transition focus:border-primary active:border-primary disabled:cursor-default disabled:bg-whiter dark:text-white dark:border-form-strokedark dark:bg-form-input dark:focus:border-primary"
              />
            </div>
            <div class="mb-5">
              <label class="mb-3 block text-black dark:text-white"> Keperluan </label>
              <input
                type="text"
                v-model="inputKeperluan"
                placeholder="Tulis Keperluan"
                class="w-full rounded-lg border-[1.5px] text-black border-stroke bg-transparent py-3 px-5 font-normal outline-none transition focus:border-primary active:border-primary disabled:cursor-default disabled:bg-whiter dark:text-white dark:border-form-strokedark dark:bg-form-input dark:focus:border-primary"
              />
            </div>
            <div class="mb-5">
              <label class="mb-3 block text-black dark:text-white"> Tanggal Pengambilan </label>
              <input
                type="date"
                v-model="inputTanggalpinjam"
                placeholder="Masukkan Nama"
                class="w-full rounded-lg border-[1.5px] text-black border-stroke bg-transparent py-3 px-5 font-normal outline-none transition focus:border-primary active:border-primary cursor-pointer disabled:bg-whiter dark:text-white dark:border-form-strokedark dark:bg-form-input dark:focus:border-primary"
              />
            </div>
            <div class="mb-5">
              <label class="mb-3 block text-black dark:text-white"> Tanggal Pengembalian </label>
              <input
                type="date"
                v-model="inputTanggalkembali"
                placeholder="Masukkan Nama"
                class="w-full rounded-lg border-[1.5px] text-black border-stroke bg-transparent py-3 px-5 font-normal outline-none transition focus:border-primary active:border-primary cursor-pointer disabled:bg-whiter dark:text-white dark:border-form-strokedark dark:bg-form-input dark:focus:border-primary"
              />
            </div>
            <div class="mb-5">
              <label class="mb-3 block text-black dark:text-white"> Jenis Alat </label>
              <input
                type="text area"
                v-model="inputAlat"
                placeholder="Masukkan Alat yang dipinjam"
                class="w-full rounded-lg border-[1.5px] text-black border-stroke bg-transparent py-3 px-5 font-normal outline-none transition focus:border-primary active:border-primary disabled:cursor-default disabled:bg-whiter dark:text-white dark:border-form-strokedark dark:bg-form-input dark:focus:border-primary"
              />
            </div>
            <div class="mb-5">
              <label class="mb-3 block text-black dark:text-white"> No Handphone </label>
              <input
                type="number"
                v-model="inputNohp"
                placeholder="Masukkan Nomor yang Bisa dihubungi"
                class="w-full rounded-lg border-[1.5px] text-black border-stroke bg-transparent py-3 px-5 font-normal outline-none transition focus:border-primary active:border-primary disabled:cursor-default disabled:bg-whiter dark:text-white dark:border-form-strokedark dark:bg-form-input dark:focus:border-primary"
              />
            </div>
            <div class="mb-5">
              <label class="mb-3 block text-black dark:text-white"> Status </label>
              <input
                type="text"
                v-model="inputStatus"
                placeholder="Ketik Keluar (untuk pengambilan)/ Masuk (untuk pengembalian)"
                class="w-full rounded-lg border-[1.5px] text-black border-stroke bg-transparent py-3 px-5 font-normal outline-none transition focus:border-primary active:border-primary disabled:cursor-default disabled:bg-whiter dark:text-white dark:border-form-strokedark dark:bg-form-input dark:focus:border-primary"
              />
            </div>

            <button
              @click="addPeminjaman"
              class="flex w-full justify-center rounded bg-primary p-3 font-medium text-gray hover:bg-opacity-90"
            >
              Kirim
            </button>
          </div>
        </DefaultCard>
        <!-- Contact Form End -->
      </div>
    </div>
    <!-- ====== Form Layout Section End -->
  </DefaultLayout>
</template>
