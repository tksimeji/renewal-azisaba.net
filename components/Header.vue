<script setup>
import {ref} from 'vue'
import {LogInIcon, MapPinnedIcon} from 'lucide-vue-next';
import {useRoute} from 'vue-router';

const route = useRoute();

const showLoginCard = ref(false)
const toggleLogin = () => {
  showLoginCard.value = !showLoginCard.value
}

const resetAll = () => {
  showMenu.value.forEach(item => {
    item.showMenu = false;
  });
}

const rules = ref([
  {name: "利用規約", showChildren: false, to: "/rules/terms"},
  {name: "Minecraftサーバ個別規定", showChildren: false, to: "/rules/minecraft-server-policy"},
  {name: "全体サーバールール", showChildren: false, to: "/rules/global-server-rules"},
  {name: "各サーバールール", showChildren: false, to: "/rules/server-rules"},
  {name: "Discordルール", showChildren: false, to: "/rules/discord"},
  {name: "チャットガイドライン", showChildren: false, to: "/rules/chat-guidelines"},
  {name: "運営登用規約", showChildren: false, to: "/rules/operating-terms-and-conditions"},
  {name: "二次創作ガイドライン", showChildren: false, to: "/rules/derivative-works-guidelines"},
]);

const connect = ref([
  {name: "接続方法", showChildren: false, to: "/connect"},
  {name: "接続アドレス", showChildren: false, to: "/connect/addresses"},
]);

const donation = ref([
  {name: "寄付ページ", showChildren: false, to: "https://store.azisaba.net/"},
  {name: "寄付に関する注意事項", showChildren: false, to: "/donation/note"},
  {name: "寄付金利用方法について", showChildren: false, to: "/donation/usage"},
  {name: "特定商取引法に基づく表記", showChildren: false, to: "/donation/commercial-transactions"},
]);

const other = ref([
  {name: "サポート", showChildren: false, to: "/support"},
  {name: "投票サイト", showChildren: false, to: "/links#投票サイト"},
  {name: "リンク", showChildren: false, to: "/links"},
]);

const showMenu = ref([
  {name: "Home", jpName: "ホーム", showMenu: false, to: "/"},
  {name: "News", jpName: "お知らせ", showMenu: false, to: "/news"},
  {name: "Join", jpName: "接続する", menu: connect, showMenu: false, to: "/connect"},
  {name: "Rule", jpName: "ルール", menu: rules, showMenu: false, to: "/rules"},
  {name: "Games", jpName: "ゲーム一覧", showMenu: false, to: "/servers"},
  {name: "Donation", jpName: "寄付", menu: donation, showMenu: false, to: "/donation"},
  {name: "Devlog", jpName: "開発ブログ", showMenu: false, to: "/devlog"},
  {name: "Others", jpName: "その他", menu: other, showMenu: false, to: "#"},
]);

const handleMenuMouseOver = async (item, event) => {
  resetAll()
  item.showMenu = true
};
</script>

<template>
  <nav class="bg-white mx-auto px-4 py-4 select-none shadow-sm w-screen">
    <div class="flex gap-8 items-center justify-between">
      <NuxtLink class="flex gap-4 items-center" to="/">
        <img alt="Server Icon" class="rounded size-8" src="@/public/icon.png"/>
        <div class="leading-none">
          <h1 class="font-semibold text-lg">アジ鯖</h1>
          <p class="text-[12px]">Azisaba Network</p>
        </div>
      </NuxtLink>

      <ul class="flex gap-2 items-center" @mouseleave="resetAll()">
        <li v-for="topLevelMenu in showMenu" :key="topLevelMenu.name">
          <NuxtLink
              class="font-semibold marker text-black/80 items-center hover:text-azisaba-dark-green/75"
              :to="topLevelMenu.to"
              @mouseover="handleMenuMouseOver(topLevelMenu, $event)"
              exact
          >
            <MapPinnedIcon
                v-if="route.path.startsWith(topLevelMenu.to) && topLevelMenu.to !== '/'"
                class="text-azisaba-dark-green/75"
                size="14"
            />
            <div v-else class="w-[14px] h-[14px]"></div>

            <span class="en">{{ topLevelMenu.name }}</span>
            <span class="jp">{{ topLevelMenu.jpName }}</span>
          </NuxtLink>
          <ul v-if="topLevelMenu.menu"
              v-show="topLevelMenu.showMenu"
              class="absolute bg-azisaba-tan flex flex-col gap-6 px-2 py-3 z-50">
            <li v-for="subMenu in topLevelMenu.menu" :key="subMenu.name">
              <NuxtLink class="font-semibold shadow-2xl text-black/70 text-md hover:underline" :to="subMenu.to" exact>
                {{ subMenu.name }}
              </NuxtLink>
            </li>
          </ul>
        </li>
      </ul>

      <Button class="bg-black" @click="toggleLogin">
        <LogInIcon size="18"/>
        ログイン
      </Button>
    </div>
  </nav>
</template>

<style scoped>
.marker {
  display: inline-block;
  min-width:75px;
  padding: 4px 6px;
  position: relative;
  text-align: center;
  text-decoration: none;
  height: 38px;
}

.marker .en {
  display: block;
  font-size: 14px;
  position: relative;
  transition: all 0.3s ease;
  z-index: 1;
}

.marker .jp {
  bottom: -2px;
  color: var(--color-azisaba-dark-green);
  font-size: 14px;
  left: 50%;
  opacity: 0;
  position: absolute;
  transition: opacity 0.3s ease, transform 0.3s ease;
  transform: translateX(-50%) translateY(100%);
  white-space: nowrap;
}

.marker:hover .en {
  font-size: 12px;
  transform: translateY(-6px);
}

.marker:hover .jp {
  opacity: 1;
  transform: translateX(-50%) translateY(0);
}

.marker::after {
  background-color: var(--color-azisaba-aqua);
  bottom: -2px;
  content: "";
  height: 2px;
  left: 0;
  position: absolute;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.3s ease;
  width: 100%;
}

.marker:hover::after {
  transform: scaleX(1);
}
</style>