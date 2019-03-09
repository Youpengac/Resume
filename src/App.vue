<template>
  <div id="app">
    <div id="content">
      <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
      <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
    </div>
    <div id="foot">
      <ThankEditor ref="thankEditor" :markdown="currentThankMarkdown" :enableHtml="enableHtml"></ThankEditor>
    </div>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import ThankEditor from './components/ThankEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor,
      ThankEditor
    },
    data() {
      return {
        interval: 5,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* 你好，我是崔有朋，我来自青岛农业大学理学与信息科学学院，信息与计算科学1701班。
* 我来写一份简单的自我介绍，希望贵校同意我的申请！谢谢！
*/

/* 给所有元素加上过渡效果 */
* {
  transition: all .1s;
}
/* 设置背景颜色 */
html {
  color: rgb(222,222,222); background: rgb(0,64,64);
}
#content{
  height:70vh;
  margin:0;
}
#foot{
  height:29vh;
  margin:0;
}

/* 设置边框 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 50vw; height: 70vh;
  background: rgb(20,20,20);
}
/* 代码高亮 */
.token.selector{ color: rgb(130,150,0); }
.token.property{ color: rgb(190,140,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(40,160,150); }

/* 加3D效果 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 50vw; height: 70vh;
  border: 1px solid;
  background: rgb(200,200,200); color: #222;
  overflow: auto;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(-10deg) translateZ(-100px) ;
          transform: rotateY(-10deg) translateZ(-100px) ;
}
/* 我要开始写啦 */
`, `
/*将Markdown格式翻译成HTML
 *再对HTML加点样式
*/
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
`, `/* 写封感谢信。
 * 感谢这一路上支持我帮助我的人。
 */
.styleEditor{
    width:50vw;height:70vh;
}

.resumeEditor{
   width:50vw;height:70vh;
}

.thankEditor{
  position: relative; left: 0; top: 0;
  background: #E9D9BB;
  color: #001C42;
  overflow: auto;
}

.thankEditor {
  width: 99vw; height: 45vh;
  border: 1px solid #ccc;
  font-size: .9em;
}
`,`
.thankEditor{
  padding: .5em;  margin: .5em; margin-top:1em;
}

.thankEditor ul,.thankEditor ol{
  list-style: none;
}
.thankEditor ul> li::before{
  content: '☞'; color: red;
  margin-right: .5em;
}
.thankEditor ol {
  counter-reset: section;
}
.thankEditor ol li::before {
  counter-increment: section;
  content: counters(section, "☞") " ";
  margin-right: .5em;
}

.thankEditor{
  width: 99vw; height: 45vh;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateX(-10deg) translateZ(-200px);
          transform: rotateX(-10deg) translateZ(-200px);
}

`],
        currentMarkdown: '',
        currentThankMarkdown: '',
        fullMarkdown: `崔有朋
====

坐标:青岛农业大学理学与信息科学学院信息与计算科学。

普通学生，专业排名倒数，不是不努力，只是因为不热爱自己专业；没有做过线下公益活动，但在网上的轻松筹捐款多次，奉献自己的爱心，感恩回馈社会。

技能
====

技术及语言
----
  - C/C++, Java SE, Android , HTML5, CSS, JS, MatLab, 图像处理, TensorFlow机器学习框架
  - Python: pandas, numpy, matplotlib
  - OS: Ubuntu, Windows
  - Others: git, Xmind, ACM竞赛算法

兴趣爱好
----
  - 打篮球, 摄影, 听音乐

链接
----

* [GitHub](https://github.com/youpengac)
* [技术博客](https://youpengac.github.io)(目前还在搭建)
* [博客园](https://www.cnblogs.com/youpeng)
* [CSDN](https://blog.csdn.net/qq_40829288)(停用但仍可访问)
* [博客园](https://www.cnblogs.com/cypblogs/)(停用但仍可访问)

联系方式
----

* 微信：hiyoupeng

`, thanksMarkdown: `
鸣谢
----

* 在我刚刚步入大学之前，我已经做好了我大学的规划。那年我高考发挥失利，暑假内心一直很难受，纠结复读还是选择上大学。但考虑到家庭情况，还是选择了后者。
* 在那段时间，我很感谢我的亲戚朋友以及我的程序员老哥一直在开导我。在选择学校时，我的程序员老哥和我一起搜集关于各所大学的信息，我想求稳，所以，对学校各方面的分析特别透彻，还做了表格进行比对，最终选择了青岛农业大学。
* 在大学的上学期，没有恪守本心，荒废了大一上学期，唯一值得庆幸的是，我这半年了解到了很多东西，拓展出去了自己的眼光，为我今后的选择打下了基础。
* 大一的寒假，我反思了自己，觉得大学不应该这样度过，大学是人生最宝贵的三年，是的，真正的大学只有三年，这三年的努力决定了后面很长的一段人生，而我，不想做一条咸鱼！
* 在那次反思之中，我知道了自己真正喜欢的东西--计算机。我第一看到代码，是高二那年暑假，在我程序员老哥的旧电脑上，不过现在成了我的旧电脑，那是很长的一段代码，就输出了我的名字这三个字。
* 从那时起，我开始对代码特别好奇，感觉这很神奇，于是，我放弃了想要选择的生物专业，毅然选择了计算机，可是不巧，我来到了数学专业。
* 很多人建议我转专业，可是我，并不想，因为我知道数学上的一些东西对我计算机上的发展是很重要的，比如研究机器学习，而我在学习图像处理的时候，用到了一些数学知识，所以，我选择留在了数学专业，做着计算机专业学生做的事，就当是免费的双学位了。
* 对计算机对技术的热爱，是从那一次长长的代码开始，始于好奇，终于热爱。在我心里，我的哥哥是一位大神，是我一直想超越的大神，也是因为他，让我对北京充满了向往，我想我一定会去北京工作，在那里写下改变世界的一行行代码。
* 从开始到现在，我还要感谢一位已经毕业的学姐，人特别好也特别优秀，对我的问题仔细耐心而且细致的给予回答，让我浮躁迷茫的内心得以平静。
* 从开始到现在，还有两位重要的人值得感谢，我的小班助，实验室的负责人学长。
* 这一路上，还有很多人，有一面之缘的，也有不再联系的朋友，也有在我心情不好时静静陪伴我的人，总之，有你们陪伴的日子都是风和日丽，谢谢。
* 可能有点跑题，对于申请，我发送的信号就是提交申请，等待学院以及贵校的返回信号，谢谢，致敬。

  `
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0);
        await this.progressivelyShowResume();
        await this.progressivelyShowStyle(1);
        await this.showHtml();
        await this.progressivelyShowStyle(2);
        await this.progressivelyShowThanks();
        await this.progressivelyShowStyle(3)
      },
      showHtml() {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) {
              return
            }
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
      },
      progressivelyShowThanks() {
        return new Promise((resolve, reject) => {
          let length = this.thanksMarkdown.length
          let interval = this.interval
          let showThanks = () => {
            if (this.currentThankMarkdown.length < length) {
              this.currentThankMarkdown = this.thanksMarkdown.substring(0, this.currentThankMarkdown.length + 1)
              let lastChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 1]
              let prevChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.thankEditor) {
                this.$nextTick(() => this.$refs.thankEditor.goBottom())
              }
              setTimeout(showThanks, interval)
            } else {
              resolve()
            }
          }
          showThanks()
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
  }

  html {
    min-height: 100vh;
  }

  * {
    box-sizing: border-box;
  }
</style>
