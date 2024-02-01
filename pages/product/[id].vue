<template>
  <br />
  <br />
  <br />

  <div>
    <h1 class="py-2 font-medium text-gray-900 dark:text-white text-center">
      Update Product
    </h1>
    <br />



    <div >
    {{   myData.data.title  }}

      <form class="max-w-sm mx-auto" @submit.prevent="submitForm()">
        <div class="mb-5">
          <label for="name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">title</label>
          <input type="text" id="title" v-model="title" name="title"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="title" />
        </div>

        <div class="mb-5">
          <label for="price" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">price</label>
          <input type="text" id="price" v-model="price" name="price"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="name" />
        </div>

        <div class="mb-5">
          <label for="image" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">image</label>
          <input type="file" id="image" ref="imageInput" @change="handleImageChange" accept="image/*" />
        </div>

        <template v-if="imageUrl">
          <img :src="imageUrl" alt="Preview Image" />
        </template>

        <button type="submit"
          class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
          Submit
        </button>
      </form>

      <br /><br />
    </div>
  </div>
</template>

<script setup>


definePageMeta({
  middleware: "auth",
});

const auth = useAuthStore();
const token = useTokenStore();
const Product = reactive({
  title: "",
  price: "",

});
const imageUrl = ref(null);
const imageInput = ref(null);



const route = useRoute();
let productId = ref(null);
const myData = ref(null);

const iteam = ref(null);



onMounted(async () => {

  productId = route.params.id;

  alert(productId);

  getProduct(productId);




});




// Define a function to fetch data
async function getProduct(productId) {
  try {
    // Fetch data using the fetch API or any other method
    const response = await fetch(`http://127.0.0.1:8000/api/products/edit/${productId}`);
    const data = await response.json();

    // Set the data to the reactive variabl

     myData.value = data;

    //  iteam.value= myData.value.data;


    console.log("Edit data:",  myData.value.data);


  } catch (error) {
    console.error('Error fetching data:', error);
  }
}







// end id

const handleImageChange = (event) => {
  const file = event.target.files[0];
  if (!file) return;

  // Validate file size and type
  if (file.size > 1024 * 1024) {
    alert("Image size too large! Max 1MB allowed.");
    return;
  }

  const reader = new FileReader();
  reader.onload = (e) => {
    imageUrl.value = e.target.result;
  };
  reader.readAsDataURL(file);
};

const submitForm = async () => {
  // const productId = this.$route.params.id;
  // console.log("User Id:", productId);
  // alert(productId);

  const formData = new FormData();
  formData.append("title", Product.title);
  formData.append("price", Product.price);
  formData.append("image", imageInput.value.files[0]);

  await useFetch(`http://127.0.0.1:8000/api/products/${id}`, {
    method: "PUT",
    body: formData,
  })
    .then(() => {
      // Success message and reset form
      alert("Product Update successfully!");
      Product.title = "";
      Product.price = "";
      imageUrl.value = null;
      imageInput.value.value = [];
    })
    .catch((error) => {
      // Error message
      console.error(error);
      alert("Error submitting form!");
    });
};
</script>

<style lang="scss" scoped></style>
