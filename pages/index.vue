<template>
  <layout-wrapper>
    <layout-visual
      title="NUXT SMAPLE SITE DEMO"
      message="お知らせやメニューをmicroCMSを導入したDEMOサイトになります。"
    />
    <div class="w-full md:max-w-3xl mx-auto pt-20 px-6 md:px-0">
      <base-heading> MdN Cafeのおすすめメニュー </base-heading>
      <div class="flex flex-wrap justify-between mb-20 md:mb-0">
        <layout-menu-list
          v-for="(item, index) in menuItems"
          :key="index"
          :image="item.image"
          :image-url="item.image.url"
          :name="item.name"
          :body="item.body"
          :price="item.price"
          item-class="md:w-56 mb-20 shadow-lg bg-gray-200"
          block-class="max-w"
          image-class="w-full"
          data-class="px-6 py-4"
          :flag-body="false"
        />
      </div>
      <div class="mx-auto mb-20 text-center">
        <nuxt-link
          class="rounded-lg px-4 md:px-5 xl:px-4 py-3 md:py-4 xl:py-3 bg-teal-500 hover:bg-teal-600 md:text-lg xl:text-base text-white font-semibold leading-tight shadow-md"
          to="/menu"
        >
          メニューの一覧
        </nuxt-link>
      </div>
      <base-heading> MdN Cafeのお知らせ </base-heading>
      <div class="mb-20">
        <layout-information-list
          v-for="(item, index) in infoItems"
          :id="item.id"
          :key="index"
          :date="item.date"
          :title="item.title"
        />
      </div>
      <div class="mx-auto mb-20 text-center">
        <nuxt-link
          class="rounded-lg px-4 md:px-5 xl:px-4 py-3 md:py-4 xl:py-3 bg-teal-500 hover:bg-teal-600 md:text-lg xl:text-base text-white font-semibold leading-tight shadow-md"
          to="/information"
        >
          お知らせの一覧
        </nuxt-link>
      </div>
    </div>
  </layout-wrapper>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData() {
    const info = await axios.get(`${process.env.API_URL}/information`, {
      headers: { 'X-API-KEY': process.env.API_KEY },
    })
    const menu = await axios.get(
      `${process.env.API_URL}/menu?limit=3&filters=flag[equals]true`,
      {
        headers: { 'X-API-KEY': process.env.API_KEY },
      }
    )
    return {
      infoItems: info.data.contents,
      menuItems: menu.data.contents,
    }
  },
}
</script>
