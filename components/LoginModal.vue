<script setup>
</script>

<template>
  <div class="bg-white grid max-w-2xl overflow-hidden rounded-xl shadow-lg w-10/12 grid-cols-[40%_60%]">
    <div
        class="bg-center bg-cover zigzag"
        style="background-image:url('https://i.azisaba.net/albums/2020-11-01_06.01.22.png')"
    ></div>

    <div class="flex flex-col gap-3 items-center justify-center p-6 text-center">
      <p>
        アジ鯖に
        <NuxtLink to="/connect">接続</NuxtLink>
        した状態で，
        Minecraftのユーザー名を入力し，ログインを押してください．
      </p>
      <Input placeholder="ユーザー名"/>
      <Input placeholder="認証コード"/>
      <Button class="w-full">ログイン</Button>
    </div>
  </div>
</template>

<style scoped>
.zigzag {
  clip-path: polygon(
      0 0, 85% 0, 90% 5%, 85% 10%, 90% 15%, 85% 20%,
      90% 25%, 85% 30%, 90% 35%, 85% 40%, 90% 45%,
      85% 50%, 90% 55%, 85% 60%, 90% 65%, 85% 70%,
      90% 75%, 85% 80%, 90% 85%, 85% 90%, 90% 95%,
      85% 100%, 0 100%
  );
}
</style>