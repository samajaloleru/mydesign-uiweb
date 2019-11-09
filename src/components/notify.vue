<template>
    <section>
        <div role="alert" class="alert" v-for="(alert, index) in notifications" :key="index"  :class="{'alert-success':alert.Code==200,'alert-danger':alert.Code!==200}"> 
            <div class="container">
                <button type="button" data-dismiss="alert" aria-label="Close" class="close">
                    <span aria-hidden="true"><i style="font-size:0.6em;" class="now-ui-icons ui-1_simple-remove"></i></span>
                </button>
                <p style="font-size:1em;text-align:left;margin-bottom:0em"  v-for="(message, msgIndex) in alert.Message.split(/\r|\n/)" :key="msgIndex">{{message.trim()}} </p>
            </div>
        </div>
    </section>
</template>

<script type="text/javascript">
  export default {
    props: ['notifications'],
    methods: {
      close(index) {
        this.$delete(this.notifications, index)
      }
    },
  }
</script>
