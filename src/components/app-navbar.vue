<template>
  <nav class="navbar navbar-expand-lg bg-primary fixed-top">
      <div class="container">
        <div class="navbar-translate">
          <a class="navbar-brand" href="" rel="tooltip" title="" data-placement="bottom" target="_blank">
      			<img class="img " src="@/assets/img/logo.png" />
          </a>
          <button class="navbar-toggler navbar-toggler" type="button" data-toggle="collapse" data-target="#navigation" aria-controls="navigation-index" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-bar bar1"></span>
            <span class="navbar-toggler-bar bar2"></span>
            <span class="navbar-toggler-bar bar3"></span>
          </button>
        </div>
        <div class="collapse navbar-collapse">
          <ul class="navbar-nav ml-auto">
            <router-link to="/">
              <li class="nav-item ">
                <a class="nav-link">
                  <h4 class="text-primary font-weight-bold">Home</h4>
                </a>
              </li>
            </router-link>
            <router-link to="/about">
              <li class="nav-item ">
                <a class="nav-link">
                  <h4 class="text-primary font-weight-bold">About Us</h4>
                </a>
              </li>
            </router-link>
            
            <router-link to="/contact">
              <li class="nav-item ">
                <a class="nav-link">
                  <h4 class="text-primary font-weight-bold">Contact Us</h4>
                </a>
              </li>
            </router-link>
          </ul>
        </div>
      </div>
  </nav>
</template>

<script>
import {HTTP} from '@/common';
import notify from "@/components/notify"
import appnavbar from "@/components/app-navbar";
import appfooter from "@/components/app-footer";
  const submenu = [        
        {to:'/',icon:'',title:'Home'},        
        {to:'/about',icon:'',title:'About Us'},        
        {to:'/contact',icon:'',title:'Contact Us'},        
        ]

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