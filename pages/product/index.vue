<template>
  <br>
  <br>
  <br>

  <!-- card start -->
  <div>
    <div
      class="w-full text-center bg-white border border-gray-200 rounded-lg shadow sm:p-3 dark:bg-gray-800 dark:border-gray-700">
      <h5 class="mb-1 text-3xl font-bold text-gray-900 dark:text-white">All Product</h5>
    </div>
  </div>
  <!-- end card -->
  <br>

 <br>
 <!-- v-if="checkPermission()" -->
<nuxt-link   to="/product/create" v-if="hasCreatePermission"> Create Product </nuxt-link>

  <div class="relative overflow-x-auto shadow-md sm:rounded-lg">

  
    <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
      <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">


        <tr>
          <th scope="col" class="px-6 py-1">Product Id</th>

          <th scope="col" class="px-6 py-1">Title</th>
          <th scope="col" class="px-6 py-1">Price</th>
          <th scope="col" class="px-6 py-1">User Name</th>

          <th scope="col" class="px-6 py-1">Action</th>
        </tr>



      </thead>
      <tbody>


        <tr v-for="(iteam, index) in dataTwice.data.data" :key="index">

      
          <th scope="row">{{ index + 1 }}</th>
          <td>{{ iteam.title }}</td>
          <td>{{ iteam.price }}</td>

          <td class="px-6 py-2">
        {{ iteam.user_id }} 
          </td>



          <td class="px-6 ">


         

            <nuxt-link   to="/product/edit"  v-if="hasEditPremission" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">
              Edit
            </nuxt-link>
          </td>

          <td class="px-6">
            <nuxt-link  to="#" v-if="hasDeletePremission" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">
            Delete   </nuxt-link>
          </td>
        </tr>
       
      </tbody>
    </table>

    <!-- <UPagination v-model="product.page" :page-count="calculatePageCount()" :total="product.total" @pageChange="fetchData" /> -->

    <UPagination v-model="page" :page-count="5" :total="20" />


  </div>


<!-- {{ permissionGet }} -->

<!-- {{ auth.getPermission.name }} -->
  <br>

  <br>
</template>


<script setup>

const page = ref(1)
const items = ref(Array(50));


const auth = useAuthStore();

let hasCreatePermission= false;
let hasEditPremission= false;
let hasDeletePremission= false;


definePageMeta({
  middleware: "auth",
});



//  onMounted=()=>{

// //   const dataTwice = await $fetch('http://127.0.0.1:8000/api/products')

// // console.log(dataTwice.data.data);
//  }

  const dataTwice = await $fetch('http://127.0.0.1:8000/api/products')

console.log("Product_Data",dataTwice.data.data);

// async asyncData({ $axios }) {
//     // Assuming you are using Axios for API requests
//     const response = await $axios.get('your-api-endpoint');

//     return {
//       productList: response.data.data,
//     };
//   },


const permissionGet = computed(() => {
  return auth.getPermission;
});
// let permissions =[]

onBeforeMount(() => {
  auth.hasCreatePremission().then(res => {
    hasCreatePermission = res;
    console.log(hasCreatePermission); // Use the value here or in subsequent code
  });




  auth.hasEditPremission().then(res => { // Use edit code
    hasEditPremission = res;
    console.log(hasEditPremission); 
  });


  auth.hasDeletePremission().then(res => {
    hasDeletePremission = res;
    console.log(hasDeletePremission); // Use the value here or in subsequent code
  });


  


});

</script>

<style lang="scss" scoped></style>
