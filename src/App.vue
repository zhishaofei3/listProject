<template>
  <div id="app">
    <Item v-for="item in articleVos" :item="item" :key="item.id"></Item>
  </div>
</template>

<script>
import Item from './Item'
import Vue from 'Vue'
export default {
  name: 'App',
  data () {
    return {
      articleVos: [
        {
          id: 96326,
          content: '<img src="http://p0.ifengimg.com/a/2018_15/e5964cd225459a0.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
        },
        {
          id: 96327,
          content: '<img src="http://p1.ifengimg.com/a/2018_15/a731e38f87c1c73.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
        },
        {
          id: 96328,
          content: '<img src="http://p1.ifengimg.com/cmpp/2018/04/10/1e9e66815165f08229dc40629bd444b9_size143_w360_h220.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
        },
        {
          id: 96329,
          content: '<img src="http://p1.ifengimg.com/a/2017_41/39fddb7091f7b72.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
        },
        {
          id: 96330,
          content: '<img src="http://p3.ifengimg.com/a/2018_15/2107c4da6445389.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
        },
        {
          id: 96331,
          content: '<img src="http://p3.ifengimg.com/a/2018_15/7da52cf474d7864.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
        },
        {
          id: 96332,
          content: '<img src="http://p1.ifengimg.com/a/2018_15/d7d2c8083ab5ef2.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
        },
        {
          id: 96333,
          content: '<img src="http://p3.ifengimg.com/a/2018_15/eab129c2e6dd786.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
        },
        {
          id: 96334,
          content: '<img src="http://p0.ifengimg.com/a/2018_15/530b50af927028e.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
        }
      ],
      id: 96334,
      isLoading: false
    }
  },
  methods: {
    onItemShow(item) {
      Vue.set(item, 'showContent', item.content)
    },
    inViewport(elem, threshold) {
      var o = elem.getBoundingClientRect()
      var pageWidth = document.documentElement.clientWidth
      var pageHeight = document.documentElement.clientHeight
      threshold = threshold || pageHeight / 5
      return o.left < pageWidth + threshold && o.top < pageHeight + threshold
    },
    onScroll() {
      let items = document.getElementsByClassName('item')
      for (let i in items) {
        let item = items[i]
        if (typeof item == 'object') {
          if (this.inViewport(item)) {
            let viewportItem = this.getItemById(item.getAttribute('id'))
            this.onItemShow(viewportItem)
          }
        }
      }

      if(window.pageYOffset + window.innerHeight >= document.documentElement.scrollHeight - 100) { //检测是否到底部
        if(!this.isLoading) {
          this.isLoading = true
          this.requestNewItem()
        }
      }
    },
    getItemById(id) {
      return this.articleVos.filter((item) => {
        return item.id == id
      })[0]
    },
    requestNewItem() {
      setTimeout(() => {
        let data = [
          {
            content: '<img src="http://p0.ifengimg.com/a/2018_15/9129453d4804b3e.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
          },
          {
            content: '<img src="http://p3.ifengimg.com/a/2018_15/866662fe7127112.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
          },
          {
            content: '<img src="http://p2.ifengimg.com/a/2018_14/dd88b8f53bf4037.jpg"><div class="tags"><a style="left: 10%; top: 20%;"></a><a style="left: 80%; top: 50%;"></a><a style="left: 40%; top: 40%;"></a></div>',
          }
        ]
        for(let i in data) {
          let item = data[i]
          item.id = ++this.id
          this.articleVos.push(item)
        }
        this.isLoading = false
      }, 1000) // 模拟ajax
    }
  },
  mounted () {
    window.addEventListener('scroll', this.onScroll)
    this.onScroll()
  },
  components: {
    Item
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>
