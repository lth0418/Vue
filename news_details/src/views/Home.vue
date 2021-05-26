<template>
  <div class="container">
      <div v-if="!info">loading</div>
      <div v-else>

        <div class="header clearfix">
        <div class="title">
            <!-- MSCI推出中国主题指数系列 涵盖颠覆性科技、未来出行等10个主题共20个指数 -->
            {{info && info.title}}
        </div>
        <div class="info">
            <span class="from">来源：{{info.originalSiteName}}</span>
            <span class="time">{{info.JMTDeploy}}</span>
        </div>
        </div>
        <div class="content" v-html="info.content">
        </div>
        <div class="function">
        <div class="report">
            <svg
            t="1621914564117"
            class="icon"
            viewBox="0 0 1127 1024"
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            p-id="3282"
            width="16"
            height="16"
            >
            <path
                d="M1108.468296 824.890547C1159.055032 910.219597 1097.227863 1024 990.429373 1024L130.432879 1024C29.258031 1024-32.574625 910.219597 18.012112 824.890547L450.825613 68.266574C473.306472 22.754136 518.276424 0 563.240888 0 608.209469 0 653.173934 22.754136 675.660283 68.266574L1108.468296 824.890547 1108.468296 824.890547 1108.468296 824.890547 1108.468296 824.890547ZM1020.384123 877.110641 1019.583053 875.735153 586.77504 119.111177 583.854223 113.62523C580.333998 106.500274 573.244216 102.4 563.240888 102.4 553.240806 102.4 546.151071 106.500212 542.636068 113.61633L539.710577 119.111663 106.096287 877.110641C95.301134 895.319767 109.937021 921.6 130.432879 921.6L990.429373 921.6C1016.30634 921.6 1031.298263 895.520476 1020.384123 877.110641L1020.384123 877.110641 1020.384123 877.110641 1020.384123 877.110641ZM558.08319 307.2C532.482248 307.2 512 322.819385 512 342.344809L512 579.251379C512 598.776801 532.482248 614.4 558.08319 614.4L568.321812 614.4C593.922749 614.4 614.4 598.776801 614.4 579.251379L614.4 342.344809C614.4 322.819385 593.922749 307.2 568.321812 307.2L558.08319 307.2 558.08319 307.2 558.08319 307.2 558.08319 307.2ZM512 766.885176C512 780.001705 517.522432 793.032632 526.999818 802.305669 536.477199 811.577487 549.797038 816.975247 563.200625 816.975247 576.602962 816.975247 589.927798 811.577487 599.405184 802.305669 608.882565 793.032632 614.4 780.001705 614.4 766.885176 614.4 753.772319 608.882565 740.741391 599.405184 731.469573 589.927798 722.19776 576.602962 716.8 563.200625 716.8 549.797038 716.8 536.477199 722.19776 526.999818 731.469573 517.522432 740.741391 512 753.772319 512 766.885176L512 766.885176 512 766.885176 512 766.885176Z"
                p-id="3283"
                fill="#cdcdcd"
            ></path>
            </svg>
            <span class="text">举报</span>
        </div>
        <div class="share">
            <svg
            t="1621913672320"
            class="icon"
            viewBox="0 0 1024 1024"
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            p-id="1994"
            width="16"
            height="16"
            >
            <path
                d="M524.032 80.128a22.208 22.208 0 1 1 0 44.416 399.488 399.488 0 1 0 399.424 399.488 22.208 22.208 0 0 1 44.416 0 443.84 443.84 0 1 1-443.84-443.904z"
                p-id="1995"
                fill="#2c2c2c"
            ></path>
            <path
                d="M816.704 267.264a22.208 22.208 0 0 1 4.032 44.032l-4.032 0.32h-115.2a155.328 155.328 0 0 0-155.072 146.88l-0.256 8.512v161.92a22.208 22.208 0 0 1-44.032 4.032l-0.32-3.968V467.008a199.744 199.744 0 0 1 190.336-199.552l9.408-0.192h115.2z"
                p-id="1996"
                fill="#2c2c2c"
            ></path>
            <path
                d="M714.368 174.08a22.4 22.4 0 0 1 27.52-4.096l4.096 3.072 108.288 101.376a22.4 22.4 0 0 1 2.88 29.44l-3.2 3.52-108.16 98.112a22.4 22.4 0 0 1-33.536-29.248l3.392-3.904 90.176-81.792-90.432-84.8a22.4 22.4 0 0 1-4.096-27.52l3.072-4.16z"
                p-id="1997"
                fill="#2c2c2c"
            ></path>
            </svg>
            <span class="text">分享</span>
        </div>
        </div>
        <div class="line"></div>
        <div class="declare">
        {{copyrightNotice}}
        </div>
        <div class="rectangle"></div>
        <div class="recommend">
        <span class="title">推荐资讯</span>
        <ul v-for="item in recommendPage.List" :key="item.id">
            <li class="article"><div>{{ item.description }}</div></li>
        </ul>
        <span class="logo"></span>
        </div>
      </div>
  </div>
</template>

<script>
import shareIcon from "../assets/img/logo.png";
import getDetail from '../api/mock';
// import dayjs from "dayjs";

export default {
  // setup() {
  //     const htmlstr = "<p>2021年4月28日，MSCI宣布推出MSCI中国主题指数系列，旨在协助投资者在瞬息万变的环境下掌握影响股票表现的中国长期结构性变化。</p><p>据悉，新推出的20个指数涵盖三大趋势类别，包括变革性技术、社会与生活方式及环境和资源。业界普遍预期这些趋势将对全球经济和社会产生深远影响。</p><p>MSCI衍生品授权及主题指数全球主管Stephane Mattatia表示，MSCI识别出促进全球经济转型、推动创新及重塑商业模式的长期结构性趋势。这些趋势增长潜力巨大，并日益成为驱动盈利和股本回报的重要因素。有别于侧重过往优胜者的传统回顾性投资方法，主题投资着眼于可能与过去截然不同的未来世界</p>"
  // return {
  //     shareIcon,
  //     htmlstr: htmlstr,
  //     items: [
  //         {message: '30省份一季报亮相 8省GDP总量超万亿 '},
  //         {message: '今年我国煤炭消费比重 将下降到56%以下 '},
  //         {message: '大宗商品还能涨多久？对制造业影响多大？...'}
  //     ]
  // }
  // },
  data() {
    return {
      info: null,
      copyrightNotice: '',
      recommendPage:null
    };
  },
  async mounted() {
     const res = await getDetail('1936897122');
     
     this.info = res.news_info;
     this.copyrightNotice = res.copyright_notice;
     this.recommendPage = res.recommend_page;
     // TODO

    // fetch("https://api.chemball.com/api/news/newsContent/findById/1936897122", {
    //   headers: {
    //     "User-Agent":
    //       "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.1 (KHTML, like Gecko) Chrome/14.0.835.163 Safari/535.1",
    //     Referer: "https://api.chemball.com/",
    //     Host: "api.chemball.com",
    //     "Access-Control-Allow-Origin": "https://api.chemball.com",
    //   },
    //   mode: "no-cors",
    // })
    //   .then((response) => {
    //       console.log(response)
    //     return response.json();
    //   })
    //   .then((response) => {
    //     this.info = response;
    //   });
  },
};
</script>


<style lang="scss">
ul,
li {
  list-style: none;
  padding: 0;
}

p {
  margin-left: 14px;
  margin-right: 15px;
  padding: 0;
}
</style>

<style lang="scss">
.container {
  width: 375px;
  .header {
    .title {
      width: 345px;
      font-weight: 500;
      font-size: 18px;
      line-height: 25px;
      letter-spacing: 1px;
      margin: 20px 15px 14px 15px;
    }
    .info {
      font-size: 12px;
      line-height: 17px;
      color: #000000;
      opacity: 0.4;
      .from {
        float: left;
        margin-left: 15px;
      }
      .time {
        float: right;
        margin-right: 15px;
      }
    }
  }
  .clearfix::after {
    content: "";
    display: block;
    clear: both;
  }
  .content {
    // width: 346px;
    // margin: 20px 15px 20px 14px;
  }
  .function {
    display: flex;
    justify-content: space-between;
    .report {
      display: flex;
      align-items: center;
      > .icon {
        margin-left: 15px;
        margin-right: 9px;
      }
      > .text {
        font-size: 14px;
        line-height: 20px;
        color: #171717;
        opacity: 0.4;
      }
    }
    .share {
      display: flex;
      align-items: center;
      > .text {
        margin-left: 8px;
        margin-right: 15px;
        font-size: 14px;
        line-height: 20px;
        color: #171717;
      }
    }
  }
  .line {
    width: 345px;
    height: 1px;
    background: #f1f1f1;
    margin: 24px 15px 15px;
  }
  .declare {
    width: 343px;
    font-size: 12px;
    line-height: 17px;
    color: #000000;
    opacity: 0.4;
    margin-left: 17px;
  }
  .rectangle {
    margin-top: 15px;
    width: 375px;
    height: 6px;
    background: #f5f5f5;
  }
  .recommend {
    margin-top: 15px;
    font-weight: 500;
    font-size: 18px;
    line-height: 25px;
    color: #000000;
    .title {
      display: block;
      margin-left: 15px;
      margin-bottom: 11px;
    }
    ul {
      .article {
        display: flex;
        align-items: center;
        height: 20px;
        font-size: 14px;
        line-height: 20px;
        color: #000000;
        margin-bottom: 12px;

        > div {
            display: -webkit-box;
            overflow: hidden;
            text-overflow: ellipsis;
            -webkit-line-clamp: 1;
            -webkit-box-orient: vertical;
        }
      }
      .article::before {
        flex: none;
        content: "";
        display: inline-block;
        width: 4px;
        height: 4px;
        margin-left: 15px;
        margin-right: 8px;
        background: #c4c4c4;
        border-radius: 50%;
      }
    }
    .logo {
      margin-left: 15px;
      display: block;
      width: 345px;
      height: 98.5px;
      background: url(../assets/img/logo.png) no-repeat center / contain;
    }
  }
}
</style>