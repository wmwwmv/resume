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
        interval: 40,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* Inspired by http://strml.net/
* 大家好，我是梁世超。
* 我来写一份简历！
*/

/* 首先给所有元素加上过渡效果 */
* {
  transition: all .3s;
}
/* 白色背景太单调了，我们来点背景 */
html {
  color: rgb(222,222,222); background: rgb(0,43,54);
}
/* 文字离边框太近了 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 45vw; height: 90vh;
}
/* 代码高亮 */
.token.selector{ color: rgb(133,153,0); }
.token.property{ color: rgb(187,137,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(42,161,152); }

/* 加点 3D 效果呗 */
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

/* 接下来我给自己准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 48vw; height: 90vh;
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
}
/* 好了，我开始写简历了 */


`,`
/* 这个简历好像差点什么
 * 对了，这是 Markdown 格式的，我需要变成对 HR 更友好的格式
 * 简单，用开源工具翻译成 HTML 就行了
 */
`,`
/* 再对 HTML 加点样式 */
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
        fullMarkdown: `梁世超
====

联系方式
====

* 电话：13106080634
* 微信：tobechaos
* 邮箱：i@liangs.me
* 网站：is.liangs.me
* [下载简历](http://d.liangs.me/resume.pdf)

教育背景
====

  - 2014-09–2018-07：辽宁工程技术大学, 软件学院, 软件工程, 工学与法学双学位.专业前5%
  - 2016-06–2016-07：中国科学院大学, 计算机与控制学院, 暑期学校, 结业.

证书
====
  - 软件设计师中级证书
  - 基于机器学习的自动摘要系统软件著作权


获奖情况
====
  - 2015-09：高教社杯全国大学生数学建模竞赛, 本科组, 全国二等奖.
  - 2016-01：Mathematical Contest In Modeling, 二等奖.
  - 2016-10：学年成绩优异.

技能
====

专业技能
----
  - 编程语言：Java > C/C++ > Python == PHP == C# > Javascript == HTML == CSS
  - 数据库：MySQL , Oracle , SQLServer , MongoDB
  - Web框架：SSH , .NET , LANMP , Django(了解) , Express(了解)
  - 数据类：有机器学习基础 , 掌握基本算法 , 会编写爬虫 , 熟悉Matlab、R、Mathematic等软件的使用
  - 软件工程：计算机基础课程 , UML等图的绘制 , 文档的撰写 , 基本的测试
  - 工具：Linux基础 , Vim、LATEX等编辑器或IDE , Git等协作工具

语言技能
----
  - 英语：CET-4，擅长读写，经常阅读英文文档、教程，常在Reddit、StackoverFlow等社区与外国人交流。
  - 普通话&闽南话：母语


工作经历
====
  - 大连中软国际有限公司	Java开发

校园经历
====
  - 辽工大CSDN高校俱乐部主席
  - 在任期间将仅有两人的社团扩充到266人,并重新搭建组织架构，拥有全校范围的影响力。社团定期举行竞赛训练，成员在各大国家级和省级赛事取得了优异成绩。另外社团和牛客网、CSDN等企业进行合作，进行技能教学、交流沙龙等活动，并举办了多次竞赛，提升了社员的学术水平、开发能力和就业层次。

毕业论文
====
  - 题目：基于复合优化的垂直搜索引擎效能提升研究
  - 导师：郭羽含
  - 说明：项目基于Heritrix、Lucene、Solr，对Heritrix和Lucene进行二次开发并重新封装，优化了Heritrix的爬取效率、简化了操作，对Lucene中的分词用正向最大匹配算法作了优化并对它的排序算法进行了一些改进，对网页使用指纹算法和相似度算法进行去重。最后使用SSH网页框架和MySql数据库完成对该系统的测试和评估以验证该项目中理论。
  - 项目地址：http://sosuo.pro

项目经历
====
  - 2014至今：萱苏茶肆
             PHP CSS3 HTML5 JQuery MySQL, 个人项目
             项目地址：http://xuansu.org
             共享计算机周边和茶叶知识的杂志站，基于wordpress，修改主题使其扁平化贴合响应式设计，设置缓存并加入二级CDN提高速度。增加了淘宝客和动态流功能，接入了微信API，可以在后台查看管理配套微信公众号数据和消息，另外还对此开发了一个微信小程序商城，可以在后台进行管理。

  - 2016：社交网络平台
          Spring Struts Hibernate JQuery MySQL, 独立项目
          项目源码：https://github.com/wmwwmv/WeTogether
          基于Java实现了日志、相册、留言板和动态流等功能，并用JQuery实现了即时通讯。用户添加好友后可以编辑自己的或者互相查看对方的个人信息、日志、相册、留言等内容而且可以实时聊天。.
          
  - 2017：基于自然语言处理和机器学习的诗歌自动生成
          Python, 独立项目.
          使用Python开发，基于自然语言处理和卷积神经网络技术自动生成有格律的古诗歌。

链接
====

* [GitHub](http://github.com/zhiiker),参与并创建过多个开源项目.
* [技术博客](http://www.zhiiker.com/)
* [另外一个博客](http://www.zhiiker.net/)

兴趣爱好及个人评价
====
  - 热爱人工智能和区块链技术，喜欢数学建模，对数字敏感，擅长用数字分析解决问题。
  - 为人坚韧乐观，自我驱动，善于沟通合作，有较强的学习能力和抗压能力，以解决技术难题为乐趣，对新技术敏感，能够尽快掌握吃透。
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
  }

  html {
    min-height: 100vh;
  }
  *{
    box-sizing: border-box;
  }
</style>
