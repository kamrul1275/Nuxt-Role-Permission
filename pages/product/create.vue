<template>
  <br>
  <br>
  <br>

  <div>

    <h1 class="py-2 font-medium text-gray-900 dark:text-white text-center">
      Create Product page
    </h1>
    <br>
  





 <div>


<!-- {{ per.name }} -->
 <h1> Create Product </h1> 



 <form class="max-w-sm mx-auto"  @click.prevent="ProductHandle()" >
      <div class="mb-5">
        <label for="name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">title</label>
        <input type="text" id="title" v-model="product.title" name="title"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="title" />
      </div>

      <div class="mb-5">
        <label for="price" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">price</label>
        <input type="text" id="email"  v-model="product.price" name="price"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="name" />
      </div>

      <div class="mb-5">
        <label for="image" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">image</label>
        <input type="file" ref="image" accept="image/*" />


</div>
      <button type="submit"
        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
        Submit
      </button>
    </form>


    <br><br>
 </div> 






  </div>
</template>




<script setup>


const auth = useAuthStore();
const token = useTokenStore();



definePageMeta({
  middleware: "permissions",
});

const permissionGet = computed(() => {
  console.log("cget_Permission",auth.getPermission);
  return auth.getPermission['/product/create'];
});



// const token = useTokenStore();
const product = reactive({
  title: "",
  price: "",
  image:"",
});
const image = ref(null);

const ProductHandle = async () => {

const formData = new FormData();
if (image.value) {
  formData.append('image', image.value.files[0]);
}

// const errors = ref([]);


  const response = await fetch('http://127.0.0.1:8000/api/products', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${token}`, // Include this line if authentication is required
  },
  body: JSON.stringify({
    title: product.title,
    price: product.price,
  }),
});


}


</script>

<style lang="scss" scoped></style>
