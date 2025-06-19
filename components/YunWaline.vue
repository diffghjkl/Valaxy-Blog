<script lang="ts" setup>
import type { WalineInitOptions } from '@waline/client'

// import { consola } from 'consola'

const customOptions: WalineInitOptions = {
  serverURL: 'https://bpl.dmoe.top',
  locale: {
        placeholder: "烦请友善交流~\n需使用超过128KB的图片时请自行使用图床", // 评论输入框内提示词（使用\n即可换行）
      },
  reaction: [], // 是否开启反应（留空即可）
  pageview: true, // 浏览量统计
  comment: true, // 评论数统计
  highlighter: true, // 代码高亮
  texRenderer: true, // 自定义数学公式处理方法，用于预览
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