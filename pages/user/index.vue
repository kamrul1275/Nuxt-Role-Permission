<template>
    <br>
    <br>    <br>    <br>    <br>
    
    <div>


<nuxt-link to="/user/create">Create User </nuxt-link>

        <div class="relative overflow-x-auto">
    <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr>
                <th scope="col" class="px-6">
                 name
                </th>
                <th scope="col" class="px-6">
                    email
                </th>
                <th scope="col" class="px-6">
                    password
                </th>

                <th scope="col" class="px-6">
                    Action
                </th>
             
            </tr>
        </thead>
        <tbody>
            <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                    Apple MacBook
                </th>
                <td class="px-6 py-4">
                    Silver@gmail.com
                </td>
                <td class="px-6 py-4">
                   54354354354
                </td>


                <td class="px-6 ">
                <nuxt-link   to="/user/edit"   class="font-medium text-blue-600 dark:text-blue-500 hover:underline">
              Edit
            </nuxt-link>
          </td>


          <td class="px-6 ">
          <nuxt-link   to="#"   class="font-medium text-blue-600 dark:text-blue-500 hover:underline">
              Delete
            </nuxt-link>
          </td>
             
            </tr>
        
        </tbody>
    </table>
</div>

    </div>
</template>
  
  
  
<script setup>



const auth = useAuthStore();

definePageMeta({
  middleware: "auth",
});



const userData = await $fetch('http://127.0.0.1:8000/api/products')

console.log("Users_Data",userData.data);





</script>

  
  <style lang="scss" scoped></style>