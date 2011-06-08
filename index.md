---
layout: english
title: Quickstart
---

# Quickstart

Springfuse reverses your database structure and generates top-quality source code that you can use immediately as the foundation of your web application.
	
To generate a project, adjust the settings below and execute the resulting command lines in a console.

<div>
<style>
table#quickstart {
	border: 1px solid gray;
}
table#quickstart tbody tr th, table#quickstart tbody tr td {
	border: 1px dotted lightgray;
}

input {
	color: black;
}
input.error {
	margin: 0.5em 0;
	padding: 0;
	background-color: red;
	color: white;
}
</style>
<div id="debug"> </div>
<table id="quickstart">
<form class="form">
	<tbody>
		<tr>
			<th>Project</th>
			<td>
				<table>
					<tbody>
						<tr>
							<th style="width:120px;">Name</th>
							<td><input type="text" id="artifactId" value="myproject" placeholder="ex: myproject" class="required lettersNumbers updateCommand" title="Use simple characters a-z, A-Z, 0-9"></td>
						</tr>
						<tr>
							<th style="width:120px;">Root package</th>
							<td><input type="text" id="groupId" size="40" value="com.company.project" placeholder="ex: com.company.project" class="required updateCommand" title="Ex: com.company.project"></td>
						</tr>
					</tbody>
				</table>
			</td>
		</tr>
		<tr>
			<th>Database</th>
			<td>
				<input type="radio" name="archetypeArtifactId" id="archetypeArtifactId3" value="quickstart-embedded-db-with-configuration" class="updateCommand" checked="checked">
				<label for="archetypeArtifactId3" title="No need to have a database, we will create an embedded database for you, and reverse it.<br/>
														Everything is done on your computer.">
					Reverse a sample database that we provide
				</label>
				<br/>
				<input type="radio" name="archetypeArtifactId" id="archetypeArtifactId1" value="quickstart" class="updateCommand">
				<label for="archetypeArtifactId1" title="You just need to provide some basic info so our plugin can reverse your database.<br/> 
														do not try this with production database, use your development database.">
					Reverse your own database
				</label>
			</td>
		</tr>
		<tr class="jdbc-properties" style="display: none">
			<th>Jdbc credentials</th>
			<td>
				Please provide your database credentials so the springfuse plugin can connect to your database and reverse it.
				<table>
					<tbody
						<tr>
							<th style="width:120px;"><label for="jdbcUrl">Url</label></th>
							<td><input type="text" name="jdbcUrl" id="jdbcUrl" size="70" class="updateCommand" placeholder="ex: jdbc:mysql://localhost/DBNAME"></td>
						</tr>
						<tr>
							<th><label for="jdbcUser">User</label></th>
							<td><input type="text" name="jdbcUser" id="jdbcUser" class="updateCommand" placeholder="ex: user"></td>
						</tr>
						<tr>
							<th><label for="jdbcPassword">Password</label></th>
							<td><input type="text" name="jdbcPassword" id="jdbcPassword" class="updateCommand" placeholder="ex: password"></td>
						</tr>
					</tbody>
				</table>
				<p class="tip">
					Do not provide here your production database credentials. 
					You should only reverse a database used for development.
					<br/>
					These settings will be used as well in the generated project to access your database.
				</p>
			</td>
		</tr>
		<tr class="jdbc-properties" style="display: none">
			<th>Jdbc driver</th>
			<td>
				Which JDBC driver should springfuse plugin use to access your database ?
				<table>
					<tbody>
						<tr>
							<th style="width:120px;"><label for="dbType">Database Vendor</label></th>
							<td>
								<select id="dbType" name="dbType" class="updateCommand">
									<option value="mysql">mysql</option>
									<option value="oracle">oracle</option>
									<option value="h2">h2</option>
									<option value="postgresql">postgresql</option>
									<option value="other">other</option>
								</select>
								<span id="oracle-database" style="display: none">
								<p class="tip">
									If you do not have an Oracle driver already in your maven repository please <a href="/install-oracle-jdbc-driver-in-maven-repository.html" target="_new">install it manually</a>.
								</p>
								</span>
								<span id="other-database" style="display: none">
								<p class="tip">
									Please replace the JDBC driver informations below with your own values.
								</p>
								</span>
							</td>
						</tr>
						<tr>
							<th><label for="jdbcGroupId">Maven groupId</label></th>
							<td><input type="text" name="jdbcGroupId" id="jdbcGroupId" size="50" class="updateCommand" placeholder="ex: mysql"></td>
						</tr>
						<tr>
							<th><label for="jdbcArtifactId">Maven artifactId</label></th>
							<td><input type="text" name="jdbcArtifactId" id="jdbcArtifactId" size="50" class="updateCommand" placeholder="ex: mysql-connector-java"></td>
						</tr>
						<tr>
							<th><label for="jdbcGroupId">Version</label></th>
							<td><input type="text" name="jdbcVersion" id="jdbcVersion" class="updateCommand" placeholder="ex: 5.1.6"></td>
						</tr>
						<tr>
							<th><label for="jdbcDriver">Driver class</label></th>
							<td><input type="text" name="jdbcDriver" id="jdbcDriver" size="50" class="updateCommand" placeholder="ex: com.mysql.jdbc.Driver"></td>
						</tr>
					</tbody>
				</table>
			</td>
		</tr>
		<tr>
			<th>Generate</th>
			<td>
				<table>
					<tr><td><input type="radio" name="frontEnd" id="jsf2Primefaces" value="jsf2Primefaces" class="updateCommand" checked="checked"></td>
						<td width="280">JSF 2, Primefaces 2.2.1, Spring Web Flow 2.3.0<br/>JPA 2 Entities/DAO/Service layers</td>
						<td>Ideal for large enterprise application requiring complex navigation, 
							extended persistence context and nice look and feel.<br/></td></tr>
					
					<tr><td><input type="radio" name="frontEnd" id="springMvc" value="springMvc" class="updateCommand"></td>
						<td>Spring MVC 3, jQuery 1.5<br/>JPA 2 Entities/DAO/Service layers</td>
						<td>A classic web stack, ideal for MDM projects.</td></tr>

					<tr><td><input type="radio" name="frontEnd"	 value="backendOnly" class="updateCommand"></td>
						<td>JPA 2 Entities/DAO/Service layers</td>
						<td>Just the backend... Ideal if you want to develop your own front end stack or if you simply don't need one.</td></tr>
				</table>
				<p>All projects uses Maven 3, Hibernate 3.5, Spring 3, Spring Security 3, Ehcache, Bean Validation etc.</p>
			</td>
		</tr>
		<tr>
			<th>Behing a proxy ?</th>
			<td>
				<input type="radio" name="proxyEnable" id="proxyEnableFalse" value="false" class="updateCommand" checked="checked">
				<label for="proxyEnableFalse">No</label>

				<input type="radio" name="proxyEnable" id="proxyEnableTrue" value="true" class="updateCommand">
				<label for="proxyEnableTrue">Yes</label>
				<div class="proxy-properties" style="display: none">
					<table>
						<tbody>
							<tr>
								<th style="width:120px;"><label for="proxyHost">Proxy hostname</label></th>
								<td><input type="text" name="proxyHost" id="proxyHost" size="50" class="updateCommand" value="intranet-proxy"></td>
							</tr>
							<tr>
								<th><label for="proxyPort">Proxy port</label></th>
								<td><input type="text" name="proxyPort" id="proxyPort" size="8" class="updateCommand" value="8080"></td>
							</tr>
							<tr>
								<th><label for="proxyUsername">Username</label></th>
								<td><input type="text" name="proxyUsername" id="proxyUsername" class="updateCommand" placeholder="ex: user"></td>
							</tr>
							<tr>
								<th><label for="proxyPassword">Password</label></th>
								<td><input type="password" name="proxyPassword" id="proxyPassword" class="updateCommand" placeholder="ex: password"></td>
							</tr>
							<tr>
								<th><label for="proxyNtlmDomain">Domain</label></th>
								<td>
									<input type="text" name="proxyNtlmDomain" id="proxyNtlmDomain" class="updateCommand" placeholder="ex: mydomain">
									<i>only if your proxy uses ntlm</i>
								</td>
							</tr>
							<tr>
								<th><label for="proxyNtlmWorkstation">Workstation</label></th>
								<td>
									<input type="text" name="proxyNtlmWorkstation" id="proxyNtlmWorkstation" class="updateCommand" placeholder="ex: mymachine"
										title="Under Windows, 
										<ul>
											<li>Open System by clicking the Start button,</li>
											<li>click on Control Panel,</li>
											<li>click on System and Maintenance,</li>
											<li>click on System.</li>
										</ul>
										You can now find your computer's name">
									<i>only if your proxy uses ntlm</i>
								</td>
							</tr>
						</tbody>
					</table>
					<p class="info">
						If not already done, please <a href="http://maven.apache.org/guides/mini/guide-proxies.html" target="_new">configure  maven to use this proxy</a> too.
					</p>
				</div>
			</td>
		</tr>
		<tr>
			<th>Advanced Configuration</th>
			<td>
				Once you get familiar with the generation process, please refer to the <a href="/documentation/springfuse.html" target="_new">code generation configuration</a> documentation to control more precisely the code generation.<br/>
			</td>
		</tr>
		<tr>
			<th><i>Your email</i></th>
			<td>
				<input type="text" id="email" placeholder="Optional" class="updateCommand" title="Used to send you personnalized tips, in case of generation failure for example.">
			</td>
		</tr>
	</tbody>
</form>
</table>
<script type="text/javascript">
	function updateDbTypeDefaultValues() {
		var urlDbType = $("#jdbcUrl").val().split(":")[1];
		var dbType = $("#dbType").val();
		if (dbType == "h2") {
			if (urlDbType != "h2") {
				$("#jdbcUrl").val("jdbc:h2:~/.h2/DBNAME");
			}
			$("#jdbcGroupId").val("com.h2database");
			$("#jdbcArtifactId").val("h2");
			$("#jdbcDriver").val("org.h2.Driver");
			$("#jdbcVersion").val("1.2.131");
		} else if (dbType == "postgresql") {
			if (urlDbType != "postgresql") {
				$("#jdbcUrl").val("jdbc:postgresql://localhost/DBNAME");
			}
			$("#jdbcGroupId").val("postgresql");
			$("#jdbcArtifactId").val("postgresql");
			$("#jdbcDriver").val("org.postgresql.Driver");
			$("#jdbcVersion").val("8.2-504.jdbc3");
		} else if (dbType == "oracle") {
			if (urlDbType != "oracle") {
				$("#jdbcUrl").val("jdbc:oracle:thin:@localhost:1521:XE");
			}
			$("#jdbcGroupId").val("com.oracle");
			$("#jdbcArtifactId").val("ojdbc14");
			$("#jdbcDriver").val("oracle.jdbc.driver.OracleDriver");
			$("#jdbcVersion").val("10.2.0.3");
		} else if (dbType == "mysql") {
			if (urlDbType != "mysql") {
				$("#jdbcUrl").val("jdbc:mysql://localhost/DBNAME");
			}
			$("#jdbcGroupId").val("mysql");
			$("#jdbcArtifactId").val("mysql-connector-java");
			$("#jdbcDriver").val("com.mysql.jdbc.Driver");
			$("#jdbcVersion").val("5.1.6");
		}

		if (dbType == "oracle") {
			$("#oracle-database").show();
		} else {
			$("#oracle-database").hide();
		}
		
		if (dbType == "other") {
			$("#other-database").show();
		} else {
			$("#other-database").hide();
		}
	}

	function param(key, value) {
		return "-D" + key + "=" + value.replace(/ /gi, "\\ ") + " ";
	}

	function updateCommand() {
		var version= "3.0.49";
		var groupId = $("#groupId").val();
		var artifactId = $("#artifactId").val();
		var email= $("#email").val();
		var frontEnd = $("input[name=frontEnd]:checked").val();
		var archetypeArtifactId = $("input[name=archetypeArtifactId]:checked").val();
		var proxyEnable = $("input[name=proxyEnable]:checked").val();

		$("#groupId").toggleClass("error", !groupId.match(/^([a-zA-Z]+){1}(\.[a-zA-Z0-9_]+)*$/));
		$("#artifactId").toggleClass("error", !artifactId.match(/^[a-zA-Z0-9]+$/));
		$("#email").toggleClass("error", email.length > 0 && !email.match(/^(\w\.\_\-])+\@([\w\.\_\-])+\.([A-Za-z]{2,4})$/));
		
		if (archetypeArtifactId == "quickstart") {
			$(".jdbc-properties").show();
		} else {
			$(".jdbc-properties").hide();
		}

		if (proxyEnable === "true") {
			$(".proxy-properties").show();
		} else {
			$(".proxy-properties").hide();
		}

		var cmd = 'mvn archetype:generate ';
		cmd += param("archetypeGroupId", "com.springfuse.archetypes");
		cmd += param("archetypeArtifactId", archetypeArtifactId);
		cmd += param("archetypeVersion", version);
		cmd += param("groupId", groupId);
		cmd += param("package", "com.springfuse.archetypes");
		cmd += param("archetypeGroupId", groupId);
		cmd += param("artifactId", artifactId);
		cmd += param("version", "1.0.0");
		cmd += param("frontEnd", frontEnd);
		cmd += param("email", email);

		if (archetypeArtifactId == "quickstart") {
			$("#cmdLine").val("");
			var jdbcGroupId = $("#jdbcGroupId").val();
			var jdbcArtifactId = $("#jdbcArtifactId").val();
			var jdbcVersion = $("#jdbcVersion").val();
			var jdbcUrl = $("#jdbcUrl").val();
			var jdbcDriver = $("#jdbcDriver").val();
			var jdbcUser = $("#jdbcUser").val();
			var jdbcPassword = $("#jdbcPassword").val();

			$("#jdbcGroupId").toggleClass("error", !jdbcGroupId.match(/^\w+(\.\w+)*$/));
			$("#jdbcArtifactId").toggleClass("error", !jdbcArtifactId.match(/^[\w\.\_\-]+$/));
			$("#jdbcVersion").toggleClass("error", !jdbcVersion.match(/^[\w\.\_\-]+$/));
			$("#jdbcUrl").toggleClass("error", !jdbcUrl.match(/^jdbc:.*/));
			$("#jdbcDriver").toggleClass("error", !jdbcDriver.match(/^[\w\.\_\-]+$/));

			cmd += param("jdbcGroupId", jdbcGroupId);
			cmd += param("jdbcArtifactId", jdbcArtifactId);
			cmd += param("jdbcVersion", jdbcVersion);
			cmd += param("jdbcDriver", jdbcDriver);
			cmd += param("jdbcUser", jdbcUser);
			cmd += param("jdbcPassword", jdbcPassword);
			cmd += param("jdbcUrl", jdbcUrl);
			$("#cmdLine").attr("rows", "14");
		} else {
			$("#cmdLine").attr("rows", "12");
		}
		cmd += param("interactiveMode", false);
		// proxy
		if (proxyEnable === "true") {
			var proxyHost = $("#proxyHost").val();
			var proxyPort = $("#proxyPort").val();
			var proxyUsername = $("#proxyUsername").val();
			var proxyPassword = $("#proxyPassword").val();
			var proxyNtlmDomain = $("#proxyNtlmDomain").val();
			var proxyNtlmWorkstation = $("#proxyNtlmWorkstation").val();

			$("#proxyHost").toggleClass("error", !proxyHost.match(/^[\w\.\_\-]+$/));
			$("#proxyPort").toggleClass("error", !proxyPort.match(/^\d+$/));

			cmd += param("proxyEnable", "true")
			cmd += param("proxyHost", "proxyHost")
			cmd += param("proxyPort", "proxyPort")
			if (proxyUsername) {
				cmd += param("proxyUsername", "proxyUsername")
				cmd += param("proxyPassword", "proxyPassword")
			}
			if (proxyNtlmDomain) {
				cmd += param("proxyNtlmEnable", "true")
				cmd += param("proxyNtlmDomain", "proxyNtlmDomain")
				cmd += param("proxyNtlmWorkstation", "proxyNtlmWorkstation")
			}
		}
		if(window.location.host.indexOf('localhost') != 0){
			cmd += param("archetypeRepository", "http://maven2.springfuse.com/")
		}
		cmd += "\n";
		cmd += 'cd ' + artifactId + '\n';
		if(window.location.host.indexOf('localhost') == 0){
			cmd += 'mvn -f springfuse.xml generate-sources -Dmaven-remote-generation-plugin.generationServiceLocation=http://localhost:9999/remote/generate\n';
		} else {
			cmd += 'mvn -f springfuse.xml generate-sources\n';
		}

		if (frontEnd !== "backendOnly") {
			$(".open-your-browser").show();
			cmd += 'mvn jetty:run\n';
		} else {
			$(".open-your-browser").hide();
			cmd += 'mvn install\n';
		}
		$("#cmdLine").val(cmd);
		$(".project-name").html(artifactId);

		$("#destinationUrl").html("<a href=\"http://localhost:8080/" + artifactId + "\">http://localhost:8080/" + artifactId + "</a>");

		if($(".error:visible").length > 0) {
			$("#cmdLine").css({"background-color": "red","color": "white"});
		} else {
			$("#cmdLine").css({"background-color": "white", "color": "black"});
		}
	}

	$(document).ready(function() {
		$(".updateCommand").change(updateCommand);
		$("#cmdLine").click(function() {
			$(this).select();
		});
		$("#jdbcUrl").change(function() {
			var dbType = $("#jdbcUrl").val().split(":")[1];
			if ($("#dbType option:contains('" + dbType + "')").val()) {
				$("#dbType").val(dbType);
			} else {
				$("#dbType").val("other")
			}
			updateDbTypeDefaultValues();
			updateCommand();
		});
		$("#dbType").change(function() {
			updateDbTypeDefaultValues();
			updateCommand();
		});
		$("#version").change(function() {
			updateCommand();
		});
		$("#frontEnd").change(function() {
			updateCommand();
		});
		
		if(window.location.href.indexOf('archetypeArtifactId=quickstart-embedded-db-with-configuration') > 0){
			$("#archetypeArtifactId3").attr('checked', true);
		} else if (window.location.href.indexOf('archetypeArtifactId=quickstart') > 0){
			$("#archetypeArtifactId1").attr('checked', true);
		}

		updateDbTypeDefaultValues();
		updateCommand();
	});
</script>
</div>

# Maven Command to Execute

Once you are done, copy-paste these maven commands lines in a console:

<textarea id="cmdLine" rows="6" cols="80" readonly="readonly" style="width:850px;height:95px" title="Cut and paste this command line to create your project"></textarea>
<p class="open-your-browser">
	Then once all is ready you can open your browser and go to <span id="destinationUrl"><a href="http://localhost:8080/myproject">http://localhost:8080/myproject</a></span>
</p>
<p class="tip">
	If the remote generation fails (error, missing entities, etc.), please <a href="/faq.html#question_remote_generation_failed" target="_new">read this faq entry</a>.
</p>

## Requirements

* JDK 1.6
* Maven 2 at least.

<p class="tip"> 
The first time you use Springfuse or Maven you may be disappointed by the time it takes to download all the jar dependencies. Just be patient...
</p>

## How It Works

Filling the form above allows you to prepare few Maven 2 commands that ultimately run your generated project!

Let's go throw the various steps:
 
The first command creates an intermediary project able to:

* reverse your database schema, or a database example we provide
* send the reversed database schema, not the data, to our server
* wait while our server generates your project
* download the generated project from our server

Then the last maven command starts the project.

For webapp project, it deploys it locally using the embedded jetty servlet container. 

For backend only project, it runs all the unit tests.

## Eclipse 

Import in eclipse, and enjoy !

<p class="tip">
Do not import the intermediary project in your IDE. Instead, import the generated project, 
its folder name ends with '-generated'.
</p>

