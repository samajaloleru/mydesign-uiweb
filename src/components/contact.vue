<template>
	<section class="">
    <appnavbar></appnavbar>  
		<div class="section" style="margin-top:70px">
      <div class="contact-content">
        <div class="container">
          <div class="row">
            <div class="col-md-5 ml-auto mr-auto">
              <h2 class="title text-primary">Send us a message</h2>
              <p class="">You can contact us for more inquiries, we will get in touch with you as soon as possible.
                <br>
                <br>
              </p>
              <form role="form" id="contact-form" method="post">
                <label>Your name</label>
                <div class="input-group">
                  <div class="input-group-prepend">
                    <span class="input-group-text"></span>
                  </div>
                  <input type="text" class="form-control" placeholder="Your Name" aria-label="Your Name..." autocomplete="name">
                </div>
                <label>Email address</label>
                <div class="input-group">
                  <div class="input-group-prepend">
                    <span class="input-group-text"></span>
                  </div>
                  <input type="email" class="form-control" placeholder="Email" aria-label="Email Here..." autocomplete="email">
                </div>
                <label>Phone</label>
                <div class="input-group">
                  <div class="input-group-prepend">
                    <span class="input-group-text"></span>
                  </div>
                  <input type="text" class="form-control" placeholder="Phone Number" autocomplete="number">
                </div>
                <div class="form-group">
                  <label>Your message</label>
                  <textarea name="message" class="form-control" id="message" rows="6"></textarea>
                </div>
                <div class="submit text-center">
                  <input type="submit" class="btn bg-primary btn-raised btn-round" value="Contact Us" />
                </div>
              </form>
            </div>
            <div class="col-md-5 ml-auto mr-auto" style="margin-top:-70px">
              <div class="info info-horizontal" style="margin-top:100px">
                <div class="icon icon-primary">
                  <i class="now-ui-icons tech_mobile"></i>
                </div>
                <div class="description  pt-4">
                  <p class="text-info"> contact@redemption-network.com
                    <br> +19169001202
                    <br> +61488896119
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
	</section>
</template>

<script>
import {HTTP} from '@/common';
import notify from "@/components/notify"
import appnavbar from "@/components/app-navbar";
import appfooter from "@/components/app-footer";

export default {
	components: {notify, appnavbar, appfooter},
	data(){ return { formSignup:{Username:"x",Password:"x",Email:""}, notifications:[]}},
	methods: {
      signup() {
		const app = this;
		if (app.formSignup.Email !== "") {
			app.formSignup.Username = app.formSignup.Email;
			app.formSignup.Password = app.formSignup.Email;
		}
        HTTP.post('/api/signup', app.formSignup ,{withCredentials: true}).then(response => {
          console.log(response)
          app.notifications.push(response.data)
		  setTimeout(checkRedirect(response.data),1500)
          if (response.data.Code == 200) {
			  app.formSignup.Username = "x";
			  app.formSignup.Password = "x";
			  app.formSignup.Email = "";
		  }
        }).catch(e => {
          console.log(e)
          this.error = e
          // this.errors.push(e)
        })
      }
    }
}
</script>