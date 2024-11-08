<script setup>
// auth
definePageMeta({
  middleware: ["auth"],
});

// supabase user param
const user = useSupabaseUser();
const supabase = useSupabaseClient();
const signOut = async () => {
  const { error } = await supabase.auth.signOut();
  if (error) console.log(error);
  router.push("/login");
};

// vue-router registry
const router = useRouter();

let { data: services, error } = await supabase.from("services").select();
</script>

<template>
  <div>
    <p class="text-sm">
      Welcome back, {{ user.name }}. Not you?
      <button @click="signOut" class="text-gray-500">Sign Out</button>
    </p>

    <ul>
      <NuxtLink to="date">
        <li
          v-for="service in services"
          :key="service.id"
          class="flex flex-row justify-between p-4 w-full items-center cursor-pointer my-2 border-2 border-gray-900 rounded-lg hover:border-emerald-500"
        >
          <div>
            <p class="font-bold text-lg">{{ service.name }}</p>
            <br />
            <p class="text-gray-500 text-sm">{{ service.description }}</p>
          </div>
          <div class="flex">
            <p class="font-bold">${{ service.price }}</p>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="size-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="m8.25 4.5 7.5 7.5-7.5 7.5"
              />
            </svg>
          </div>
        </li>
      </NuxtLink>
    </ul>
  </div>
</template>
