<template>
	<section class="">
		<appnavbar></appnavbar> 
			<div class="section" style="margin-top:70px">
        <div class="container">
          <div class="row">
            <div class="col-md-9 ml-auto mr-auto">
              <h3 class="display-5">About Us:</h3>
              <p>Redemption Network is focused on bringing Relief, Freedom, and Accomplishment to people all around the globe. These are just a few of the positive emotional effects of debt — once they are paid off, that is it.
                <br /> This is the mission of Redemption Network.</p>
              <p> “Debt freedom isn’t just freedom from debt. It’s freedom from worry.” Redemption network has been set up by a group of philanthropists who want to give back to the world they have immensely benefited from, to help different people all over the world overcome their debt thereby offering a brand new start to both the young and the old that have been dealing with the burden of debt. In the past 3 years, Redemption network has touched the lives of over 10 million people across 5 continents and 20 countries. 
                    We want to unlock the possibility inside every individual, change the world for people and enable them in their unique capacity to change the world and also touch the lives of others around them.
								<br/>It is a help cycle where you get help and also help others hence spreading the happiness to a good number of people in no time.
								<br/>At Redemption network, Every person has the opportunity to achieve his/her fullest potential and participate in making better the lives of others
							</p>
              <p> We are also set to help people with outstanding business ideas push it to a reality upon evaluation of their ideas. Having founded and worked for several entrepreneurial businesses, our philantropists understand how difficult it can be to raise money to start and grow a small business. The task of securing an investment is a notoriously perplexing and sometimes sluggish process that can be a struggle at the best of times. In today's economic climate this has become even more challenging. 
								<br/>Comprehensive business ideas/proposals can be sent in to <span class="font-weight-bold text-success"> contact@redemption-network.com</span> for thorough analysis by our team of skilled and experienced specialists. Once passed, you're halfway to making your dream business a reality. 
							</p>
              <p> We believe Charity is a necessity and not an option. Bounty is said to receive a part of its value from the manner in which it is bestowed. The act of compassion and generosity can be big or small but their echoes are endless.
								<br/><br/>You also can have a brand new start! 
								<br/><br/>Reach us at <span class="font-weight-bold text-success"> contact@redemption-network.com</span> and let us take it from there.</p>
            </div>
          </div>
        </div>
      </div>		
		<appfooter></appfooter>
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