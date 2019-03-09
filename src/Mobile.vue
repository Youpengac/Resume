<template>
  <div id="app">
    <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
    <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor
    },
    data() {
      return {
        interval: 5,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* 你好，我是崔有朋，我来自青岛农业大学理学与信息科学学院，信息与计算科学1701班。
* 我来写一份简单的自我介绍，希望贵校同意我的申请！
*/

/* 给所有元素加上过渡效果 */
* {
  transition: all .2s;
}
/* 设置背景颜色 */
html {
  color: rgb(222,222,222);
  background: rgb(0,43,54);
}
/* 设置边框 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  overflow: auto;
  width: 90vw;
  margin: 2.5vh 5vw;
  height: 90vh;
}
/* 太高了 */
.styleEditor {
  height: 45vh;
}
/* 代码高亮 */
.token.selector{
  color: rgb(133,153,0);
}
.token.property{
  color: rgb(187,137,0);
}
.token.punctuation{
  color: yellow;
}
.token.function{
  color: rgb(42,161,152);
}

/* 加3D效果 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  transform: rotateX(-10deg) translateZ(-50px) ;
}

/* 准备一个编辑器 */
.resumeEditor{
  position: fixed;
  top: 50%; left: 0;
  padding: .5em;  margin: 2.5vh;
  width: 95vw; height: 45vh;
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
}
/* 开始写我的简单自我介绍 */


`,
          `
/*将Markdown格式翻译成HTML
 *再对HTML加点样式
*/
`, `
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`],
        currentMarkdown: '',
        fullMarkdown: `崔有朋

====

坐标:青岛农业大学理学与信息科学学院信息与计算科学。

普通学生，专业排名倒数，没有做过线下公益活动，但在网上的轻松筹捐款多次，奉献自己的爱心，感恩回馈社会。

技能
====

技术及语言
----
  - Java: SpringMVC, SpringCloud, Hibernate, iBatis, spark, sql2o, HikariCP, freemarker, okHttp, retrofit, RxJava
  - Kotlin: ktor, exposed, anko
  - Node.js: express, angular, ionic, react, cordova, meteor, electron, axios
  - Swift: Vapor, ReactiveSwift
  - Golang: hugo, beego, gorm, sqlx, matcha
  - Python: tushare, pandas, numpy, matplotlib
  - DotNet and PHP
  - DB: SQLServer, Oracle, MySQL/MariaDB, MongoDB, graphQL, redis, memcached
  - WebServer: apache, nginx, tomcat, netty, jetty
  - OS: Ubuntu, CentOS, MacOS, Windows
  - Others: Docker, git, Xmind，Axure

链接
----

* [GitHub](https://github.com/youpengac)
* [技术博客](http://youpengac.github.io(目前还在搭建)
* [博客园](http://www.cnblogs.com/youpeng)
* [CSDN](https://blog.csdn.net/qq_40829288（停用但仍可访问)
* [博客园](http://www.cnblogs.com/cypblogs(停用但仍可访问)

联系方式
----

* 微信：hiyoupeng

\`, thanksMarkdown: \`
鸣谢
----

* 在我刚刚步入大学之前，我以及做好了我大学的规划，我高考发挥失利，那段时间内心一直很难受，纠结复读还是选择上大学，但考虑到家庭情况，已经没有复读的资格。
* 在那段时间，我和感谢我的程序员哥哥一直在开到我，和我一起在网上搜罗了各种各种学校的资料，我想求稳，所以，对学校各方面的分析特别透着，甚至做了表格进行比对，最终选择了青岛农业大学。
* 来到大学的上学期，有点随波逐流，我承认我忘掉了自己之前的规划，所以，大一上学期，我给自己的评价是虚度光阴。
* 大一的寒假，我反思了自己，觉得大学不应该这样度过，大学是人生最宝贵的三年，是的，真正的大学只有三年，这三年的努力决定了后面很长的一段人生。
* 也就是在那次反思之中，我知道了自己真正喜欢的东西--计算机，我第一看到代码，是高二那年暑假，在我程序员老哥的旧电脑上，不过现在成了我的旧电脑，那是很长的一段代码，就输出了我的名字这三个字。
* 从那时起，我开始对代码特别好奇，感觉这很神奇，于是，我放弃了决定选择的生物专业，依然选择了计算机，可是不巧，我来到了数学专业。
* 很多人建议我转专业，可是我，并不想，因为我知道数学上的一些东西对我计算机上的发展是很重要的，比如研究机器学习，所以，我留在了数学专业，做着计算机专业学生做的事。
* 对计算机对技术的热爱，从那一次长长的代码开始，始于好奇，终于热爱。在我心里，我的哥哥是一位大神，是我一直想超越的大神，也是因为他，让我对北京充满了向往，我想我一定会去北京工作，在那里写下改变世界的一行行代码。

  `
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0)
        await this.progressivelyShowResume()
        await this.progressivelyShowStyle(1)
        await this.showHtml()
        await this.progressivelyShowStyle(2)
      },
      showHtml: function () {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          this.$nextTick(() => {
            this.$refs.resumeEditor.goTop()
          })
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) { return }
            // 计算前 n 个 style 的字符总数
            let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
            let prefixLength = length - style.length
            if (this.currentStyle.length < length) {
              let l = this.currentStyle.length - prefixLength
              let char = style.substring(l, l + 1) || ' '
              this.currentStyle += char
              if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
                this.$nextTick(() => {
                  this.$refs.styleEditor.goBottom()
                })
              }
              setTimeout(showStyle, interval)
            } else {
              resolve()
            }
          }).bind(this)
          showStyle()
        })
      },
      progressivelyShowResume() {
        return new Promise((resolve, reject) => {
          let length = this.fullMarkdown.length
          let interval = this.interval
          let showResume = () => {
            if (this.currentMarkdown.length < length) {
              this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
              let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
              let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.resumeEditor) {
                this.$nextTick(() => this.$refs.resumeEditor.goBottom())
              }
              setTimeout(showResume, interval)
            } else {
              resolve()
            }
          }
          showResume()
        })
      }
    }
  }

</script>

<style scoped>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    min-height: 100vh; position: relative;
  }

  html {
    min-height: 100vh;
  }
  *{
    box-sizing: border-box;
  }

</style>
