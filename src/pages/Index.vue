<template>
  <Layout>
    <!-- Page Header -->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(http://localhost:1337${$page.general.cover.url})`,
      }"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{ $page.general.title }}</h1>
              <span class="subheading">{{ $page.general.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div
            class="post-preview"
            v-for="edge in $page.posts.edges"
            :key="edge.node.id"
          >
            <g-link :to="'/post/' + edge.node.id">
              <h2 class="post-title">
                {{ edge.node.title }}
              </h2>
              <h3 class="post-subtitle">
                Problems look mighty small from 150 miles up
              </h3>
            </g-link>
            <p class="post-meta">
              Posted by
              <a href="#">{{ edge.node.create_by.username }}</a>
              on {{ edge.node.created_at }}
            </p>
            <p>
              <g-link
                :to="'/tag/' + tag.id"
                v-for="tag in edge.node.tags"
                :key="tag.id"
                >{{ tag.title }}</g-link
              >
            </p>
            <hr />
          </div>

          <Pager :info="$page.posts.pageInfo" />
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query ($page: Int) {
  posts: allStrapiPosts (perPage: 2, page: $page) @paginate {
    pageInfo {
      currentPage
      totalPages
    }
    edges {
      node {
        id
        title
        cover {
          url
        }
        content
        tags {
          id
          title
        }
        created_at
        create_by {
          username
        }
      }
    }
  }

  general: strapiGeneral(id:1) {
    title
    subtitle
    cover {
      url
    }
  }
}

</page-query>  

<script>
import { Pager } from "gridsome";
export default {
  name: "HomePage",
  metaInfo: {
    title: "Hello, world!",
  },
  components: {
    Pager,
  },
};
</script>

<style>
</style>
