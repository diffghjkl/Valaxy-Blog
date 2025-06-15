<script lang="ts" setup>
import type { WalineInitOptions } from '@waline/client'

// import { consola } from 'consola'

const customOptions: WalineInitOptions = {
  serverURL: 'https://bpl.dmoe.top',
  pageview: true, // 浏览量统计
  comment: true, // 评论数统计
  reaction: false, // 是否开启反应
  emoji: [
        '//unpkg.com/@waline/emojis@1.2.0/bilibili',
        '//unpkg.com/@waline/emojis@1.2.0/bmoji',
        '//unpkg.com/@waline/emojis@1.2.0/tieba',
        '//unpkg.com/@waline/emojis@1.2.0/qq',
      ],

// 自定义图片上传功能（未开启时默认使用Base64嵌入评论）
  // imageUploader: (file) => {
  //   consola.info('Upload file: ', file)

  //   const formData = new FormData()
  //   const headers = new Headers()

  //   formData.append('file', file)
  //   headers.append('Authorization', '!{API TOKEN}')
  //   headers.append('Accept', 'application/json')
  // 使用时请将 '!{API TOKEN}' 部分修改为图床的API Token

  //   return fetch('!{API URL}', {
  //     method: 'POST',
  //     headers,
  //     body: formData,
  //   })
  //     .then(resp => resp.json())
  //     .then(resp => resp.data.links.url)
  // },
  // 使用时请将 '!{API URL}' 部分修改为图床的上传接口，如 https://sm.ms/api/v2/upload
}
</script>

<template>
  <WalineClient w="full" :options="customOptions" />
</template>