<script>
  import AOS from "aos"
  import 'aos/dist/aos.css'
  AOS.init()
  import axios from 'axios'
  export default{
    data(){
        return {
            value:"",
            nomor:"",
        }
    },
    methods:{
      // getData(){
      //   this.$router.push("/admin")
      //   // alert("HALOOOOO")
      // },
      login (){
            if(this.value.length < 1){
                alert("Data Tidak Boleh Kosong")
            } else {
                let result =  axios.post("http://localhost:4000/login",{
                "nama":this.value,    
                "alamat":this.nomor,
                }).then(response =>{
                  console.log(response.data)
                  if(`${response.data}` == "ADA KESALAHAN COBA LAGI"){
                        alert(`${response.data}`)
                        localStorage.setItem("autenticated", false)
                        this.$router.push("/login")
                  } else if (`${response.data}` == "BERHASIL LOGIN") {
                    // alert(`${response.data}`)
                    localStorage.setItem("autenticated", true)
                    this.$router.push("/admin")
                  }
                })
                // alert("Anda Telah login")
                // this.$router.push("/admin")
            }
        },
    }
  }
</script>

<template>
<div data-aos="fade-up" data-aos-delay="1000">
    <div class=" h-24  items-center flex justify-center">
      <div class="w-fit flex justify-center font-bold text-white text-xl text-center"> SELAMAT DATANG DI WEB IURAN PERUMAHAN  </div>
  </div>
  <div class="w-full px-40">
      <input v-model="value" class="shadow appearance-none border rounded w-full py-6 px-3 mt-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="nama" type="text" placeholder="Masukkan Email">
      <p class="font-bold text-white"> Value: {{ value }}</p>
      <input v-model="nomor" class="shadow appearance-none border rounded w-full mt-4 py-6 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="nomor" type="text" placeholder="Masukkan Password">
      <p class="font-bold text-white"> Value: {{ nomor }}</p>
    </div>
    <div class="grid justify-items-center p-2 ">
        <button @click="login" class="bg-green-500 hover:bg-gray-400 text-white font-bold py-2 px-4 rounded inline-flex items-center">
            Login
        </button>
     </div>
  </div>

</template>

<style>
  body{
    background-color: #1e293b;;
  }
</style>'
