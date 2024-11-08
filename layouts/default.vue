<script setup>
const user = useSupabaseUser();
const supabase = useSupabaseClient();
const signOut = async () => {
  const { error } = await supabase.auth.signOut();
  if (error) console.log(error);
  router.push("/login");
};
</script>
<template>
  <div>
    <header class="flex justify-end px-4 py-2">
      <button @click="signOut" v-show="user">Sign Out</button>
    </header>
    <div class="md:flex gap-10 full mx-4 md:mx-16">
      <div class="w-full"><slot /></div>
      <Sidebar class="md:w-1/3" v-show="user" />
    </div>
  </div>
</template>

<style>
.full {
  height: 100%;
}
</style>
