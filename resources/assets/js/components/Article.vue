<template>
    <div id="app">
        <div class="container expecial">
            <div class="container-fluid">
                <div class="jumbotron text-center">
                    <div class="row">
                        <div class="col-md-10 col-md-offset-1"><h1 data-v-06a33fa2="">Nothing is
                            impossible.</h1>
                            <h3 data-v-06a33fa2="">欢迎加入LaravelChen讨论群</h3></div>
                    </div>
                </div>
            </div>
        </div>
        <div class="container">
            <div class="row">
                <div class="col-md-10 col-md-offset-1">
                    <article class="post post-list" v-for="article in articles">
                        <h1 class="title">
                            <router-link :to="{ name: 'article', params: { id: article.id }}"tag="a">{{ article.title }}</router-link>
                        </h1>
                        <div class="entry-content">
                            <p class="blog-content">{{article.body | excerpt}}[...]</p>
                            <p>
                                <router-link :to="{ name: 'article', params: { id: article.id }}"tag="a" class="color-grey comment"><i class="fa fa-comment-o"></i>{{article.comments_count}}条评论</router-link>
                                <router-link :to="{ name: 'article', params: { id: article.id }}"tag="a" class="color-grey comment"><i class="fa fa-thumbs-o-up"></i>点赞数({{article.votes_count}})</router-link>
                                <router-link :to="{ name: 'article', params: { id: article.id }}"tag="a" class="more-link pull-right">继续阅读 »</router-link>
                            </p>
                        </div>
                    </article>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default{
          name: 'app',
          data:function(){
             return {
                articles:[],
             }
          },
           filters: {
                excerpt: function (value) {
                   var str= value.replace(/<\/?[^>]*>/g,'');
                   return str.substring(0,250);
                }
            },
          mounted:function(){
             this.$http.get('/api/article').then((response)=>{
                   this.articles=response.data;
             })
          }
    }

</script>
