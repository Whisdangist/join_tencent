<template>
  <div class="home">
    <div class="bg">
      <div class="bg_items">
        <div class="bg_0"></div>
        <div class="bg_1"></div>
        <div class="bg_2"></div>
        <div class="bg_3"></div>
      </div>
      <div class="wave_items">
        <div v-for="i in 8" :key=i :style="`animation-delay: ${i * 0.8}s`"></div>
      </div>
    </div>
    <div class="container">
      <div class="header">
        <a href="/" class="logo"></a>
        <ul class="nav">
          <li class="active"><a href="/">首页</a></li>
          <li><a href="#" @click="banner_id = 1">岗位详情</a></li>
          <li><a href="/news">通知动态</a></li>
          <li><a href="/about">了解腾讯</a></li>
          <li><a href="/video">视频干货</a></li>
        </ul>
        <div class="members">
          <div class="nolog">
            <a href="#" @click="login">登录</a>
          </div>
        </div>
      </div>
      <div class="banners" @wheel="wheelBanner">
        <div data-id="0" class="banner news" :class="{ 'active': banner_id === 0 }">
          <div class="slogan animated bounceIn"></div>
          <div class="slogan_title animated bounceIn"></div>
          <div class="timeline animated bounceIn">
            <div class="wrap_timeline">
              <div class="wrap_process_bar">
                <div class="wrap_process_circle">
                  <div class="process_circle"></div>
                </div>
              </div>
              <div class="wrap_timeline_text">
                <div class="time_point">
                  <div class="date">8.1-9.15</div>
                  <div class="process">网申</div>
                </div>
                <div class="time_point">
                  <div class="date">8.1-9.12</div>
                  <div class="process">提前批</div>
                </div>
                <div class="time_point">
                  <div class="date">详见通知动态</div>
                  <div class="process">在线笔试</div>
                </div>
                <div class="time_point" style="color: #fffe00;">
                  <div class="date">9.26</div>
                  <div class="process">常规批</div>
                </div>
              </div>
            </div>
          </div>
          <div class="btns">
            <a class="btn_s" href="#" @click="showBanner(1)">投递简历</a>
            <a class="btn_k" href="https://join.qq.com/news_detail.php?id=220">流程FAQ</a>
          </div>
        </div>
        <div data-id="1" class="banner jobs" :class="{ 'active': banner_id === 1 }">
          <div class="wrap_jobs">
            <div class="campus_recruitment animated slideInRight">
              <div class="wrap_job_bg">
                <div class="job_bg" :class="{ 'animate_job_right': animate_campus }"></div>
              </div>
              <div class="job_post" @mouseover="animate_campus=true" @mouseleave="animate_campus=false">
                <h2 class="job_title" :style="{ 'transform': `translateY(${animate_campus ? '0' : '20%'})` }"></h2>
                <ul class="job_list" :class="{ 'animated fadeInDownSmall': animate_campus }" :style="{ 'opacity': Number(animate_campus) }">
                  <li><a href="/post">校园招聘</a></li>
                  <li><a href="https://careers.tencent.com/MBA.html" target="_blank">MBA招聘</a></li>
                </ul>
              </div>
            </div>
            <div class="intern_recruitment animated slideInRight">
              <div class="wrap_job_bg">
                <div class="job_bg" :class="{ 'animate_job_right': animate_intern }"></div>
              </div>
              <div class="job_post" @mouseover="animate_intern=true" @mouseleave="animate_intern=false">
                <h2 class="job_title" :style="{ 'transform': `translateY(${animate_intern ? '0' : '20%'})` }"></h2>
                <ul class="job_list" :class="{ 'animated fadeInDownSmall': animate_intern }" :style="{ 'opacity': Number(animate_intern) }">
                  <li><a href="/post">暑期实习</a></li>
                  <li><a href="/post">日常实习</a></li>
                  <li><a href="/post">Pre留学生实习</a></li>
                </ul>
              </div>
            </div>
          </div>
        </div>
        <div data-id="2" class="banner talks" :class="{ 'active': banner_id === 2 }">
          <div class="wrap_talks">
            <!-- <a href="https://v.qq.com/variety/p/topic/txwotalk2018/index.html" target="_blank"></a> -->
            <div class="cont_talks">
              <a href="https://join.qq.com/news_detail.php?id=232" target="_blank">
                <div class="bg_talks animated slideInRight"></div>
              </a>
            </div>
          </div>
        </div>
        <div class="btns_slider" data-num="3">
          <a href="#" class="btn_prev" :style="{ 'display': banner_id > 0 ? 'block' : 'none' }" @click="banner_id--"></a>
          <a href="#" class="btn_next" :style="{ 'display': banner_id < 2 ? 'block' : 'none' }" @click="banner_id++"></a>
        </div>
      </div>
    </div>
    <div class="wrap_buttons">
      <div class="sm">
        <div class="i" :class="{ 'active0': banner_id === 0, 'active1': banner_id === 1, 'active2': banner_id === 2}"></div>
      </div>
      <ul class="buttons">
        <li data-id="0" :class="{ 'active': banner_id === 0 }" @click="banner_id = 0">校招动态</li>
        <li data-id="1" :class="{ 'active': banner_id === 1 }" @click="banner_id = 1">在招岗位</li>
        <li data-id="2" :class="{ 'active': banner_id === 2 }" @click="banner_id = 2">犀牛鸟精英计划</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      animate_campus: false,
      animate_intern: false,
      banner_id: 0,
      wheeling: false
    }
  },
  methods: {
    login: function () {
      window.alert('不要在奇奇怪怪的网站登陆QQ号噢！！！')
    },
    wheelBanner: function (event) {
      if (!this.wheeling) {
        this.wheeling = true
        if (event.deltaY > 0 && this.banner_id < 2) {
          this.banner_id++
        } else if (event.deltaY < 0 && this.banner_id > 0) {
          this.banner_id--
        }
        setTimeout(() => { this.wheeling = false }, 500)
      }
    }
  }
}
</script>

<style lang="stylus">
  .home
    width: 100%
    height: 100%
    .bg
      position: absolute
      z-index: 0
      background: url(bg.png) no-repeat
      background-size: cover
      width: 100%
      height: 100%
      .bg_items
        & > *
          position: absolute
          animation-timing-function: linear
          animation-iteration-count: infinite
        .bg_0
          background: url(bg-0.png) center center no-repeat
          background-size: cover
          width: 100%
          height: 100%
          opacity: 0.8
          animation-name: rotating_week_animate
          animation-duration: 10s
          @keyframes rotating_week_animate
            0%
              transform: translate3d(0, 0, 0) scale(1, 1)
            50%
              transform: translate3d(10px, 0, 0) scale(1, 1)
            100%
              transform: translate3d(0, 0, 0) scale(1, 1)
        .bg_1
          background: url(bg-1.png) right bottom no-repeat
          background-size: cover
          width: 80%
          height: 160%
          left: 0
          margin-left: -20%
          bottom: -30%
          opacity: 0.9
          animation-name: rotating_back_animate
          animation-duration: 30s
          @keyframes rotating_back_animate
            0%
              transform: rotate(0) scale(1)
            25%
              transform: rotate(-6deg) scale(0.9) translate3d(10px, -10px, 0)
            50%
              transform: rotate(-2deg) scale(1.1)
            75%
              transform: rotate(-6deg) scale(0.9) translate3d(10px, -10px, 0)
            100%
              transform: rotate(0) scale(1)
        .bg_2
          background: url(bg-2.png) right bottom no-repeat
          background-size: contain
          width: 80%
          height: 80%
          left: -40%
          bottom: 75%
          animation-name: rotating_animate
          animation-duration: 20s
          @keyframes rotating_animate
            0%
              transform: rotate(0) scale(1)
            50%
              transform: rotate(6deg) scale(0.9, 1.1) translate3d(10%, -16%, 30px)
            100%
              transform: rotate(0) scale(1)
        .bg_3
          background: url(bg-3.png) no-repeat
          width: 613px
          height: 607px
          right: -270px
          bottom: 65%
          animation-delay: 0.5s
          animation-name: rotating_all_animate
          animation-duration: 100s
          @keyframes rotating_all_animate
            0%
              transform: rotate(0) scale(1) translate3d(0, 0, 0)
            25%
              transform: rotate(90deg) scale(1.3, 0.6) translate3d(-10px, -40px, -10px)
            50%
              transfrom: rotate(0) scale(1, 1) translate3d(40px, -20px, 20px)
            75%
              transform: rotate(90deg) scale(1.2, 0.8) translate3d(-10px, -40px, 10px)
            100%
              transform: rotate(0) scale(1) translate3d(0, 0, 0)
      .wave_items
        position: absolute
        width: 80%
        overflow: visible
        margin: auto
        left: 0
        right: 0
        top: 50%
        margin-top: -40%
        &:after
          content: ''
          display: block
          margin-top: 100%
        & > *
          position: absolute
          border: 1px solid #63c8f4
          border-radius: 50%
          margin: auto
          left: 0
          right: 0
          top: 0
          bottom: 0
          opacity: 0
          animation-name: wave_animate
          animation-duration: 10s
          animation-iteration-count: infinite
          animation-timing-function: ease-out
          @keyframes wave_animate
            0%
              opacity: 0
              transform: scale(0.2)
            20%
              opacity: 0.9
            60%
              opacity: 0.1
            100%
              opacity: 0
              transform: scale(1)
    .container
      position: relative
      z-index: 1
      width: 100%
      min-width: 1024px
      height: 100%
      min-height: 500px
      .header
        position: absolute
        left: 100px
        right: 100px
        top: 50px
        margin: auto
        max-width: 1600px
        z-index: 300
        a
          color: #fff
          opacity: 0.8
          &:hover
            opacity: 1
        .logo
          display: block
          background: url(logo.png) center center no-repeat
          background-size: contain
          width: 230px
          @media screen and (max-width: 1279px)
            width: 180px
          height: 31px
          float: left
          margin-right: 40px
          opacity: 1
        .nav
          font-size: 1.6rem
          float: left
          margin-top: 6px
          a
            display: block
            float: left
            padding-bottom: 8px
          .active
            a
              opacity: 1
              font-weight: bold
              border-bottom: 2px solid #ffffff
          li
            margin: 0 2.2rem
            @media screen and (max-width: 1279px)
              margin: 0 1.2rem
            float: left
        .members
          position: absolute
          top: 6px
          right: 0
      .banners
        position: relative
        width: 100%
        height: 100%
        overflow: hidden
        & > .banner
          display: none
          &.active
            display: block
          position: relative
          width: 100%
          height: 100%
        .news
          .slogan
            background: url(home_main.png) center center no-repeat
            background-size: contain
            width: 54%
            height: 54%
            margin: auto
            position: absolute
            top: 0
            bottom: 0
            left: 0
            right: 0
          .slogan_title
            background: url(slogan0723.png) center center no-repeat
            background-size: contain
            width: 32%
            height: 32%
            margin: auto
            position: absolute
            top: -10%
            bottom: 0
            left: 0
            right: 0
            animation-delay: 0.4s
          .timeline
            width: 60%
            height: 15%
            background-size: contain
            margin: auto
            position: absolute
            top: 60%
            left: 0
            right: 0
            animation-delay: 0.2s
            .wrap_timeline
              transform: skew(0, -6deg)
              text-align: center
              width: 80%
              margin: 0 auto
              .wrap_process_bar
                width: 100%
                height: 5px
                margin-bottom: 20px
                background: url(bg_process_bar.png) center center no-repeat
                background-size: contain
                .wrap_process_circle
                  width: 72.8%
                  height: 100%
                  position: relative
                  background: linear-gradient(to right, #fff62000, #fff620)
                  .process_circle
                    background: url(process_circle.png)
                    background-size: contain
                    width: 34px
                    height: 34px
                    position: absolute
                    top: -12px
                    right: -12px
              .wrap_timeline_text
                padding: 0 20%
                line-height: normal
                .time_point
                  width: 25%
                  float: left
                  font-size: 1.8rem
          .btns
            position: absolute
            top: 80%
            left: 0
            right: 0
            margin: auto
            width: 380px
            @media screen and (max-width: 1279px)
              width: 304px
            & > *
              display: block
              border-radius: 28px
              float: left
              width: 168px
              height: 56px
              line-height: 56px
              @media screen and (max-width: 1279px)
                width: 130px
                height: 42px
                line-height: 42px
              text-align: center
              text-decoration: none
              font-size: 2rem
            .btn_s
              background: #fff200
              &:hover
                background: #efe300
              color: #0765c8
              margin-right: 40px
            .btn_k
              &:hover
                background: rgba(255, 255, 255, 0.1)
              border: 1px solid #fff
              color: #fff
        .jobs
          background: rgba(6, 169, 208, 0.65)
          .wrap_jobs
            position: absolute
            top: 0
            bottom: 0
            left: 0
            right: 0
            margin: auto
            width: 70%
            height: 46%
            max-height: 700px
            & > *
              position: relative
              float: left
              width: 36%
              height: 90%
              padding: 5%
              background-color: #fff
              border-radius: 10px
              animation-duration: 0.3s
              .wrap_job_bg
                position: absolute
                right: 0
                bottom: -10%
                width: 110%
                height: 100%
                overflow: hidden
                .job_bg
                  position: absolute
                  right: 0
                  bottom: 0
                  width: 100%
                  height: 90%
                  transition-duration: 0.3s
                  &.animate_job_right
                    transform: translateX(10%)
                    opacity: 0.5
              .job_post
                position: relative
                height: 100%
                border-radius: 10px
                .job_title
                  transition-duration: 0.4s
                .job_list
                  opacity: 0
                  font-size: 1.2em
                  line-height: 60px
                  margin-top: 40px
                  @media screen and (max-width: 1279px)
                    margin-top: 30px
                  margin-left: 4px
                  text-align: left
                  li > a:hover
                    color: #d9b572
                  &.fadeInDownSmall
                    animation-name: fadeInDownSmall
                    @keyframes fadeInDownSmall
                      from
                        opacity: 0
                        transform: translate3d(0, -10%, 0)
                      to
                        opacity: 1
                        transform: translate3d(0, 0, 0)
            .campus_recruitment
              .wrap_job_bg
                .job_bg
                  background: url(bg_job_left.png) bottom right no-repeat
                  background-size: auto 100%
              .job_post
                top: 0
                left: 0
                .job_title
                  background: url(xyzp.png) no-repeat
                  background-size: contain
                  width: 205px
                  height: 60px
                  @media screen and (max-width: 1279px)
                    width: 140px
                    height: 50px
            .intern_recruitment
              float: right
              animation-delay: 0.1s
              .wrap_job_bg
                .job_bg
                  background: url(bg_job_right.png) bottom right no-repeat
                  background-size: auto 100%
              .job_post
                top: 0
                right: 0
                .job_title
                  background: url(sxszp.png) no-repeat
                  background-size: contain
                  width: 256px
                  height: 60px
                  @media screen and (max-width: 1279px)
                    width: 150px
                    height: 50px
        .talks
          background: rgba(169, 0, 255, 0.65)
          .wrap_talks
            position: absolute
            left: 0
            right: 0
            top: 0
            bottom: 0
            margin: auto
            width: 90%
            max-width: 1400px
            height: 70%
            .cont_talks
              position: absolute
              left: 0
              right: 0
              top: 0
              bottom: 0
              margin: auto
              width: 100%
              height: 100%
              .bg_talks
                background: url(bg_talks_1210.png) center center no-repeat
                background-size: contain
                animation-duration: 0.5s
                position: absolute
                left: 0
                right: 0
                top: 0
                bottom: 0
                margin: auto
                width: 100%
                height: 100%
                @media screen and (max-width: 1279px)
                  width: 86%
                  height: 90%
        .btns_slider
          & > *
            display: block
            position: absolute
            top: 50%
            width: 26px
            height: 47px
            opacity: 0.9
            &:hover
              opacity: 1
          .btn_prev
            background: url(btn_prev.png) center center no-repeat
            left: 60px
          .btn_next
            background: url(btn_next.png) center center no-repeat
            right: 60px
    .wrap_buttons
      position: absolute
      z-index: 1
      left: 0
      bottom: 0
      width: 100%
      border-top: 1px solid rgba(255, 255, 255, 0.3)
      .sm
        position: relative
        margin: 0 auto
        width: 80%
        .i
          position: absolute
          display: block
          left: 0
          top: -2px
          width: 33.33%
          height: 4px
          border-radius: 2px
          background: #fff
          transition-duration: 0.3s
          &.active0
            transform: translateX(0)
          &.active1
            transform: translateX(100%)
          &.active2
            transform: translateX(200%)
      .buttons
        padding: 0 100px
        width: 80%
        max-width: 1600px
        margin: 0 auto
        li
          position: relative
          height: 80ox
          line-height: 80px
          @media screen and (max-height: 768px)
            height: 50px
            line-height: 50px
          cursor: pointer
          float: left
          width: 33.33%
          text-align: center
          opacity: 0.5
          &.active
            opacity: 1
          &:hover
            opacity: 1
</style>
