<template>
  <div class="paragraph">
    <h3>{{ content.metadata.pres_title }}</h3>
    <div class="begin">{{ pres_first }}</div>
    <p>{{ pres_second }}</p>
  </div>
</template>

<script>
export default {
  name: "Description",
  props: ["content"],
  data: () => ({
    pres_first: `エンジニアを目指す修士1年生。\n大学院では、数学を専攻。好きな公式は、オイラー積の公式！笑`,
    pres_second:
      "大学の授業では、C,Python,JavaScriptを学習。\n現在は、Vue.js,TypeScriptを勉強中…",
  }),
};
</script>

<style scoped lang="scss">
@import "@/styles/constants.scss";

.paragraph {
  color: map-get($colors, primary);
  .begin {
    color: map-get($colors, secondary);
  }
}
</style>
