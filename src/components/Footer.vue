<template>
  <footer>
    <div class="copyright">
      <n-text class="description" v-html="packageJson.description" />
      <n-text
        class="author"
        :depth="3"
        v-html="packageJson.author"
        @click="jumpLink(packageJson.github)"
      />
    </div>

    <!-- 新增的一行 -->
    <n-text :depth="3" class="more-info">
      <span @click="jumpLink(links.own)">Own By {{ links.ownName }}</span>
      |
      <span @click="jumpLink(links.built)">Built By {{ links.builtName }}</span>
      |
      <span @click="jumpMail(links.mail)">Contact Me By Email</span>
    </n-text>

    <n-text
      v-if="icp"
      :depth="3"
      class="icp"
      v-html="icp"
      @click="jumpLink('https://icp.gov.moe/?keyword=20250850')"
    />
  </footer>
</template>

<script setup>
import packageJson from "@/../package.json";

const links = {
  own: 'https://artemisia.icu',
  ownName: 'Artemisia',
  built: 'https://github.com/artemisia1107',
  builtName: 'artemisia1107',
  mail: 'artemisia666@foxmail.com'   // QQ 邮箱
}

const icp = ref(import.meta.env.VITE_ICP ? import.meta.env.VITE_ICP : null);

// 链接跳转
const jumpLink = (url) => {
  window.open(url);
};
const jumpMail = (email) => (
  window.location.href = `mailto:${email}`
)
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
  .more-info {
    font-size: 13px;
    cursor: pointer;
    transition: all 0.3s;
    &:hover {
      color: var(--n-code-text-color);
    }
  }
  .copyright {
    margin-bottom: 4px;
    .description {
      &::after {
        content: "@ License By";
        margin: 0 6px;
      }
    }
  }
  .author {
    cursor: pointer;
    transition: all 0.3s;
    &:hover {
      color: var(--n-code-text-color);
    }
  }
  .icp {
    font-size: 13px;
    cursor: pointer;
    transition: all 0.3s;
    &:hover {
      color: var(--n-code-text-color);
    }
  }  
}
</style>
