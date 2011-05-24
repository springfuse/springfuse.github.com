---
layout: english
title: Contact us 
---

# Contact us
<div id="questionnaire">
	<style>
		form#contact_form label {
			display: inline-block;
			width:100px;
			padding: 0;
			text-align: right;
		}
		form#contact_form label.required {
			font-weight: bold;
		}
	</style>
       	<form action="https://spreadsheets.google.com/spreadsheet/formResponse?formkey=dFBRSzJDeWZaZWJyV2ozS3FEX3Zld2c6MQ&amp;ifq&amp;theme=0AX42CRMsmRFbUy03NTAzM2Q4My03ODU1LTQ2NzItODI2YS1kZmU5YzdiMzZjOGQ" 
			method="POST" id="contact_form" target="google_form" onsubmit="submitted=true;">
		<input type="hidden" name="pageNumber" value="0"/>
		<input type="hidden" name="backupCache"/>
		<fieldset>
			<p>
				<label for="firstname" class="required">Firstname</label>
				<input id="firstname" type="text" name="entry.0.single" placeholder="Required" required/>
			</p>
			<p>
				<label for="lastname" class="required">Lastname *</label>
				<input id="lastname" type="text" name="entry.2.single" placeholder="Required" required/>
			</p>
			<p>
				<label for="email" class="required">Email *</label>
				<input id="email" type="email" name="entry.4.single" placeholder="Required" required/>
			</p>
			<p>
				<label for="title">Title</label>
				<input id="title" type="text" name="entry.9.single" placeholder="Optional"/>
				<label for="company">Company</label>
				<input id="company" type="text" name="entry.11.single" placeholder="Optional"/>
				<label for="phone">Phone</label>
				<input id="phone" type="phone" name="entry.6.single" placeholder="Optional"/>
			</p>
			<p>
				<label for="message" class="required" style="vertical-align:top;">Message</label>
				<textarea id="message" name="entry.8.single" placeholder="Please enter your message..." style="width:570px;height: 150px;" required></textarea>
			</p>
			<p>
				<input type="submit" name="submit" value="Send" style="float:right;padding:5px;font-size:15px;width:200px;border: 1px solid #BEBEBE;background-color: white;"/><br>
			</p>
		</fieldset>
	</form>
</div>
<div id="confirmation" style="display: none" class="notice">
We got your message, we will get back to you shortly.
</div>

<!-- see http://www.morningcopy.com.au/tutorials/how-to-style-google-forms/ -->
<script type="text/javascript">
	var submitted=false;
	function formLoaded() {
		if(submitted) {
			$("#questionnaire").hide();
			$("#confirmation").show();
		} 
	}
</script>
<iframe name="google_form"
	style="display:none;"
	src="https://spreadsheets.google.com/embeddedform?formkey=dDVxTzhZY0tfaXNoYWVCV0RvWHJWd1E6MQ" 
	onload="formLoaded();">
		Loading...
</iframe>
