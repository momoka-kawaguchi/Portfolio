<template>
  <section id="experience">
    <AnimateOnVisible name="fadeDown" :duration="1">
      <Title
        :class="title"
        :title="content.metadata.title"
        description="Education and Learning"
      >
      </Title>
    </AnimateOnVisible>

    <AnimateOnVisible name="fadeUp" :duration="1">
      <div class="container-fluid">
        <div class="row">
          <ExperienceColumn
            :posts="educations"
            title="Education"
            class="col-12 col-md left"
          />
          <ExperienceColumn
            :posts="learning"
            title="Learning"
            class="col-12 col-md right"
          />
        </div>
      </div>
    </AnimateOnVisible>
  </section>
</template>

<script>
import Title from "./Title.vue";
import ExperienceColumn from "./ExperienceColumn.vue";

export default {
  name: "Experience",
  props: ["content"],
  data: () => ({
    educations: [
      {
        year: "March 2018",
        title: "高校卒業",
        content:
          "高校3年次には、イギリスのCambridge大学に短期留学を経験。\n高大連携教育として、大学での授業や研究活動を行なった。",
      },
      {
        year: "April 2018",
        title: "大学入学",
        content:
          "理工学部数学科に進学。純粋数学と情報数学を学ぶ。",
      },
      {
        year: "March 2022",
        title: "大学卒業 ＆ 教員免許取得",
        content:
          "大学卒業と同時に、数学と情報の中高教員免許を取得。",
      },
      {
        year: "April 2022",
        title: "大学院入学",
        content:
          "理工学研究科数学専攻に進学。代数学を研究。",
      },
    ],
     learning: [
      {
        year: "April 2017",
        title: "プログラミングとの出会い",
        content:
          "高大連携教育として、週に1度大学(数学)の教授との研究を始める。\nBASICを用いて、初めてユークリッドの互除法のプログラムを制作。\n高校卒業時には、暗号技術についての研究発表を行う。",
      },
      {
        year: "April 2018",
        title: "大学での講義",
        content:
          "大学では、C言語、JavaScript、Pythonを用いた授業を受講。\n主に情報技術におけるアルゴリズムについて学習する。",
      },
       {
        year: "April 2019",
        title: "Latexでレポート提出",
        content:
          '数学の講義レポートを提出する際に、マークアップ言語であるLaTexを用いて、資料を作成。\nまた、ICT教材であるGeoGebra、Wintpic、Mathematicaを用いて、動的教材を提案する。',
      },
       {
        year: "April 2022",
        title: "本格的な勉強！",
        content:
          "本格的にプログラミングを学びたいと思い、継続的に学習することを決意。\nProgateやUdemyを活用して、HTML、CSS、JavaScriptの学習を始める。\nまた、Vue.jsやGatsby(React)を用いて、ポートフォリオを作成。",
      },
    ],
  }),
  components: {
    Title,
    ExperienceColumn,
  },
};
</script>

<style scoped lang="scss">
@import "@/styles/constants.scss";

$linear: map-get($colors, dark);

#experience {
  background-color: lighten(map-get($colors, primary), 5%);
}

.title {
  color: map-get($colors, light);
}

.row {
  padding-top: 20px;
  text-align: center;
}

.css-test {
  white-space: pre-wrap;
}

@media (min-width: #{map-get($breakpoints, small)}) {
  .left {
    text-align: right;
    border-right: 2px solid $linear;
  }
  .right {
    text-align: left;
  }
}

@media (max-width: #{map-get($breakpoints, small)}) {
  .right {
    margin-top: 20px;
  }
  .left:before {
    content: "";
    position: absolute;
    left: 20%;
    bottom: 0;
    height: 2px;
    width: 60%; /* or 100px */
    border-bottom: 2px solid $linear;
  }
}

/deep/ .text-wrapper {
  &:after {
    border-bottom: 1px solid map-get($colors, dark);
  }
}
</style>
