<script>
  import { butter } from '@/buttercms'
  export default {
    name: 'customer-page',
    data() {
      return {
        slug: this.$route.params.slug,
        page: {
          slug: '',
          fields: {}
        }
      }
    },
    methods: {
      getPage() {
        butter.page.retrieve('customer_case_study', this.slug)
          .then((res) => {
            console.log(res.data.data)
            this.page = res.data.data
          }).catch((res) => {
          console.log(res)
        })
      }
    },
    created() {
      this.getPage()
    }
  }
</script>
And, just like you did for the case studies homepage, you need to display the content by defining a template and calling the content fields you want to show:

<template>
  <div id="customer-page">
    <figure>
      <img :src="page.fields.customer_logo">
    </figure>
    <h1>{{ page.fields.headline }}</h1>
    <h3>Testimonials</h3>
    <div v-html="page.fields.testimonial"></div>
    <div v-html="page.fields.body"></div>
  </div>
</template>
