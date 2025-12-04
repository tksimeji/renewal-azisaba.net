<script setup>
const minecraftId = ref('');
const loginCode = ref('');
const step = ref('request');

const handleRequestCode = async () => {
  const response = await fetch('http://localhost:8080/v1/auth/request-code', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({minecraftId: minecraftId.value}),
  });

  if (!response.ok) {
    const errorText = await response.text();
    throw new Error(`HTTP error! status: ${response.status}, body: ${errorText}`);
  }

  step.value = 'verify';
};

const handleVerify = async () => {
  const response = await fetch('http://localhost:8080/v1/auth/verify-code', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({minecraftId: minecraftId.value, code: loginCode.value}),
    credentials: 'include',
  });

  if (!response.ok) {
    const errorText = await response.text();
    throw new Error(`HTTP error! status: ${response.status}, body: ${errorText}`);
  }

  const response2 = await fetch('http://localhost:8080/v1/auth/me', {
    method: 'GET',
    headers: {
      'Content-Type': 'application/json'
    },
    credentials: 'include',
  });
  const user = await response2.text();
  console.log(user);
};

</script>

<template>
  <div class="bg-white grid h-80 max-w-2xl overflow-hidden rounded-xl shadow-lg w-10/12 grid-cols-[40%_60%]">
    <div
        class="bg-center bg-cover zigzag"
        style="background-image:url('https://i.azisaba.net/albums/2020-11-01_06.01.22.png')"
    ></div>

    <div class="flex flex-col gap-3 items-center justify-center p-6 text-center">
      <template v-if="step === 'request'">
        <p>
          アジ鯖に
          <NuxtLink to="/connect">接続</NuxtLink>
          した状態で，
          Minecraftのユーザー名を入力し，ログインを押してください．
        </p>
        <Input placeholder="Minecraft ID" v-model="minecraftId"/>
        <PrimaryButton class="w-full" @click="handleRequestCode">認証コードを送信</PrimaryButton>
      </template>
      <template v-else>
        <p>{{ minecraftId }}にチャットで認証コードを送信しました．</p>
        <Input placeholder="認証コード" v-model="loginCode"/>
        <PrimaryButton class="w-full" @click="handleVerify">ログイン</PrimaryButton>
      </template>
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