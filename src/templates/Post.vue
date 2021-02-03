<template>
  <Layout>
    <!-- Page Header -->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(http://localhost:1337${$page.post.cover.url})`,
      }"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{ $page.post.title }}</h1>
              <!-- <h2 class="subheading">
                Problems look mighty small from 150 miles up
              </h2> -->
              <span class="meta"
                >Posted by
                <a href="#">{{ $page.post.create_by.username }}</a>
                on August 24, 2019</span
              >
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Post Content -->
    <article>
      <div class="container">
        <div class="row">
          <div
            class="col-lg-8 col-md-10 mx-auto"
            v-html="markToHtml($page.post.content)"
          ></div>
        </div>
      </div>
    </article>
  </Layout>
</template>

<script>
import markdown from "markdown-it";

const md = new markdown();

export default {
  name: "PostPage",
  methods: {
    markToHtml(mdStr) {
      return md.render(mdStr);
    },
  },
};
</script>

<style>
</style>

<page-query>
query ($id: ID!)  {
	post: strapiPosts (id: $id) {
    id
    title
    create_by {
      username
    }
    content
    cover {
      url
    }
  }
}
</page-query>