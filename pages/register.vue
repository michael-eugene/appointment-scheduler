<script setup>
const supabase = useSupabaseClient();
const router = useRouter();

const email = ref("");
const password = ref(null);
const errorMsg = ref(null);
const successMsg = ref(null);

const signUp = async () => {
  const { data, error } = await supabase.auth.signUp({
    email: email.value,
    password: password.value,
  });
  if (error) {
    console.log(error);
  } else {
    router.push("/login");
  }
};
</script>

<template>
  <div>
    <div class="bg-gray-50" style="height: 100vh">
      <div
        class="flex min-h-[80vh] flex-col justify-center py-12 sm:px-6 lg:px-8"
      >
        <div class="text-center sm:mx-auto sm:w-full sm:max-w-md">
          <h1 class="text-3xl font-extrabold text-gray-900">Sign Up!</h1>
        </div>
        <div class="mt-8 sm:mx-auto sm:w-full sm:max-w-md">
          <div
            class="bg-white px-4 pb-4 pt-8 sm:rounded-lg sm:px-10 sm:pb-6 sm:shadow"
          >
            <form class="space-y-6" @submit.prevent="signUp">
              <div>
                <label
                  for="email"
                  class="block text-sm font-medium text-gray-700"
                  >Email:</label
                >
                <div class="mt-1">
                  <input
                    v-model="email"
                    type="email"
                    required
                    class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-emerald-500 focus:outline-none focus:ring-emerald-500 sm:text-sm"
                  />
                </div>
              </div>
              <div>
                <label
                  for="password"
                  class="block text-sm font-medium text-gray-700"
                  >Password:</label
                >
                <div class="mt-1">
                  <input
                    v-model="password"
                    name="password"
                    type="password"
                    autocomplete="current-password"
                    required
                    class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-emerald-500 focus:outline-none focus:ring-emerald-500 sm:text-sm"
                  />
                </div>
              </div>
              <div>
                <label
                  for="password"
                  class="block text-sm font-medium text-gray-700"
                  >Confirm Password:</label
                >
                <div class="mt-1">
                  <input
                    type="password"
                    required
                    class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-emerald-500 focus:outline-none focus:ring-emerald-500 sm:text-sm"
                  />
                </div>
              </div>
              <div>
                <button
                  type="submit"
                  class="group relative flex w-full justify-center rounded-md border border-transparent bg-emerald-600 px-4 py-2 text-sm font-medium text-white hover:bg-emerald-700 focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:ring-offset-2 disabled:cursor-wait disabled:opacity-50"
                >
                  <span
                    class="absolute inset-y-0 left-0 flex items-center pl-3"
                  >
                    <svg
                      class="h-5 w-5 text-emerald-500 group-hover:text-emerald-400"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                      aria-hidden="true"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M5 9V7a5 5 0 0110 0v2a2 2 0 012 2v5a2 2 0 01-2 2H5a2 2 0 01-2-2v-5a2 2 0 012-2zm8-2v2H7V7a3 3 0 016 0z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                  </span>
                  Sign Up
                </button>
              </div>
            </form>
            <div class="m-auto mt-6 w-fit md:mt-8">
              <span class="m-auto"
                >Already have an account?
                <a class="font-semibold text-emerald-600" href="/login"
                  >Log In</a
                >
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped></style>
