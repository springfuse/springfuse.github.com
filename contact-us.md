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
			text-align:right;
		}
		form#contact_form label.required {
			font-weight:bold;
		}
		form#contact_form label.error {
			width:200px;
			margin-bottom: 0;
			padding: 0;
			
		}
	</style>
	<form action="https://spreadsheets.google.com/spreadsheet/formResponse?formkey=dDVxTzhZY0tfaXNoYWVCV0RvWHJWd1E6MQ&amp;theme=0AX42CRMsmRFbUy03NTAzM2Q4My03ODU1LTQ2NzItODI2YS1kZmU5YzdiMzZjOGQ" 
			method="POST" id="contact_form" target="google_form" onsubmit="submitted=true;">
		<input type="hidden" name="pageNumber" value="0"/>
		<input type="hidden" name="backupCache" value=""/>
		<fieldset>
			<p>
				<label for="firstname" class="required">Firstname</label>
				<input id="firstname" type="text" name="entry.0.single" value=""/>
				<label for="lastname" class="required">Lastname *</label>
				<input id="lastname" type="text" name="entry.2.single" value="" class="email"/>
			</p>
			<p>
				<label for="email" class="required">Email *</label>
				<input id="email" type="text" name="entry.10.single" value=""/>
				<label for="phone">Phone</label>
				<input id="phone" type="text" name="entry.8.single" value=""/>
			</p>
			<p>
				<label for="Message" class="required" style="vertical-align:top;">Message</label>
				<textarea id="message" name="entry.4.single" style="width:500px;height: 150px;"></textarea>
			</p>
			<p>
				<center>
					<input type="submit" name="submit" value="Send" style="padding:5px;font-size:15px;width:150px;border: 1px solid #BEBEBE;background-color: white;"/>
				</center>
			</p>
		</fieldset>
	</form>
	<script type="text/javascript">
		$(document).ready(function() {
			$("#contact_form").validate({
				rules: {
					firstname: "required",
					lastname: "required",
					email: {
						required: true,
						email: true
					},
					message: {
						required: true,
						minlength: 5
					}
				}
			});
		});
	</script>
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
