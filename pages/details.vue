<script setup>
const user = useSupabaseUser();
const router = useRouter()

const checkOut = () => {
router.push('/checkout')
}
</script>
<template>
  <div>
    <div class="flex items-center mb-4">
      <NuxtLink to="date"
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          strokeWidth="{1.5}"
          stroke="currentColor"
          class="size-6"
        >
          <path
            strokeLinecap="round"
            strokeLinejoin="round"
            d="M15.75 19.5 8.25 12l7.5-7.5"
          />
        </svg>
      </NuxtLink>
      <p class="text-2xl font-bold">Confirm your details!</p>
    </div>

    <form @submit.prevent="checkOut" class="form flex flex-col gap-4">
      <div>
        <input required type="text" placeholder="First Name" id="first_name" class="" />
        <input required type="text" placeholder="Last Name" id="last_name" class="" />
      </div>
      <div class="text-gray-500">{{ user.email }}</div>

      <label for="terms"
        ><input type="radio" id="terms" required /> Accept Terms & Conditions</label
      ><br />
      <input type="submit"
        class="bg-emerald-500 text-white rounded-lg py-2 w-full" value="Continue"
      >
    </form>
  </div>
</template>
