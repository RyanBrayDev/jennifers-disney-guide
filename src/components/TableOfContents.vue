<template>
  <div class="table-of-contents">
    <ul v-scroll-spy-active v-scroll-spy-link>
      <li v-for="content in contents" :key="content.id">
        <a>{{ content.anchorText }}</a>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: "TableOfContents",
    data: function () {
      return {
        contents: [],
      }
    },
    mounted() {
      var elements = document.getElementsByClassName('toc-content');
      var newContents = [];
      for (var i = 0; i < elements.length; i++) {
        if (elements[i].firstChild.innerText) {
          newContents.push({
            id: elements[i].id,
            anchorText: elements[i].firstChild.innerText
          });
        }
        else {
          newContents.push({
            id: elements[i].firstChild.id,
            anchorText: elements[i].firstChild.firstChild.alt
          });
        }
      }
      this.contents = newContents;
    }
  }
</script>

<style scoped>

  .active{
    color: yellow;
  }

  .table-of-contents {
    background-color: red;
    border-radius: 5px;
    border: 2px solid yellow;
    padding: 20px;
    position: fixed;
    width: 210px;
    color: white;
    display: none;
  }

  .table-of-contents a {
    text-decoration: none;
    font-size: 25px;
    display: block;
    margin-bottom: 10px;
    padding: 5px;
    border-radius: 5px;
  }

  .table-of-contents a:hover {
    background-color: yellow;
    color: black;
  }

  .table-of-contents ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }

  @media (min-width: 768px) {
    .table-of-contents {
      display: block;
    }
  }

  @media screen and (max-height: 550px) {
    .table-of-contents {
      padding-top: 14px;
    }

    .table-of-contents a {
      font-size: 18px;
      line-height: 18px;
    }
  }

</style>
