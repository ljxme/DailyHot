<template>
  <footer>
    <!-- 1. 第二行提前到最上面 -->
    <n-text :depth="3" class="more-info">
      Own By
      <span class="link" @click="jumpLink(links.own)">{{ links.ownName }}</span>
      |
      Built By
      <span class="link" @click="jumpLink(links.built)">{{ links.builtName }}</span>
      |
      Contact Me By
      <span class="link" @click="jumpMail(links.mail)">Email</span>
    </n-text>

    <!-- 2. 原来的版权行 -->
    <div class="copyright">
      <n-text class="description" v-html="packageJson.description" />
      <n-text
        class="author"
        :depth="3"
        v-html="packageJson.author"
        @click="jumpLink(packageJson.github)"
      />
    </div>

    <!-- 3. 备案信息 -->
    <n-text
      v-if="icp"
      :depth="3"
      class="icp"
      v-html="icp"
      @click="jumpLink('https://beian.miit.gov.cn/')"
    />
  </footer>
</template>

<script setup>
import packageJson from '@/../package.json'

const links = {
  own: 'https://artemisia.icu',
  ownName: 'Artemisia',
  built: 'https://github.com/artemisia1107',
  builtName: 'artemisia1107',
  mail: 'artemisia666@foxmail.com'
}

const icp = ref(import.meta.env.VITE_ICP || null)

const jumpLink = (url) => window.open(url)
const jumpMail = (email) => (window.location.href = `mailto:${email}`)
</script>

<style lang="scss" scoped>
footer {
  height: 100px;
  padding: 0 5vw;
  max-width: 1800px;
  margin: 20px auto 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 4px;              // 行与行之间一点间距

  .more-info {
    font-size: 13px;
    color: var(--n-text-color-base);
    .link {
      cursor: pointer;
      transition: color 0.3s;
      &:hover { color: var(--n-code-text-color);
                text-decoration: underline;
              }
    }
  }

  .copyright {
    display: flex;
    align-items: center;
    .description::after {
      content: "@ License By";
      margin: 0 6px;
    }
  }

  .author {
    cursor: pointer;
    transition: color 0.3s;
    &:hover { color: var(--n-code-text-color); }
  }

  .icp {
    font-size: 13px;
    cursor: pointer;
    transition: color 0.3s;
    &:hover { color: var(--n-code-text-color); }
  }
}
</style>
