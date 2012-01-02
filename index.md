---
layout: english
title: SpringFuse - Online Java Code Generator
---

# SpringFuse: Online Java Code Generator

SpringFuse is the online version of <a href="http://www.jaxio.com/en/celerio.html">Celerio</a>,
a code generation tool for Java developed by <a href="http://www.jaxio.com/en/">Jaxio</a>. It reverses your database structure and generates top-quality Java source code that you 
can use immediately as the foundation of your web application.
	
<strong>To generate a project, adjust the settings below and execute the resulting command lines in a console.</strong>

Requirements: Have at least Java 1.6 and Maven 2 installed on your machine.

<div>
	<g:plusone></g:plusone>
</div>

Current version: 3.0.69 (<a href="/change-log.html">change logs</a>).

We announce new version on twitter: <a href="http://twitter.com/#!/springfuse">@springfuse</a>

## Step 1/4: Fill the code generation form 

<div>
<style>
table#quickstart {
	border: 1px solid gray;
}
table#quickstart tbody tr th {
	border: 1px dotted lightgray;
	font-weight:bold;
}

table#quickstart tbody tr td {
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
			<th><i>Your email</i></th>
			<td>
				<input type="text" id="email" class="required updateCommand"> We send to this email the code generation logs and the extracted metadata.
			</td>
		</tr>		
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
							<th style="width:120px;">Java root package</th>
							<td><input type="text" id="groupId" size="40" value="com.jaxio.demo" placeholder="ex: com.jaxio.demo" class="required updateCommand" title="Ex: com.company.project"></td>
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
					Reverse a sample H2 database that we provide
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
									<option value="db2">db2</option>
									<option value="h2">h2</option>
									<option value="postgresql">postgresql</option>
									<option value="other">other</option>
								</select>
								<span id="oracle-database" style="display: none">
								<p class="tip">
									If you do not have an Oracle driver already in your maven repository please <a href="/install-oracle-jdbc-driver-in-maven-repository.html" target="_new">install it manually</a>.
								</p>
								<p class="tip">
									If you rely on sequences to generate your PK ids, you must configure Celerio during 'Step 3/4' below. Please refer to 'Use a SEQUENCE per TABLE' section in the <a target="_new" href="http://www.springfuse.com/documentation/pdf/springfuse.pdf">documentation</a>.
								</p>								
								</span>
								<span id="db2-database" style="display: none">
								<p class="tip">
									If you do not have an DB2 driver already in your maven repository please <a href="/reverse-db2-database-schema.html" target="_new">install it manually</a>.
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
							<td><input type="text" name="jdbcVersion" id="jdbcVersion" class="updateCommand" placeholder="ex: 5.1.17"></td>
						</tr>
						<tr>
							<th><label for="jdbcDriver">Driver class</label></th>
							<td><input type="text" name="jdbcDriver" id="jdbcDriver" size="50" class="updateCommand" placeholder="ex: com.mysql.jdbc.Driver"></td>
						</tr>
					</tbody>
				</table>
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
		<tr>
			<th>Generation&nbsp;Output</th>
			<td>
				<table>
					<tr><td><input type="radio" name="frontEnd" id="jsf2Primefaces" value="jsf2Primefaces" class="updateCommand" checked="checked"></td>
						<td width="280">Web application project using: <br/>JSF 2, Primefaces 3.0, Spring WebFlow 2.3.0<br/>JPA 2 Entities/DAO/Service layers</td>
						<td>Ideal for large enterprise application requiring complex navigation, 
							extended persistence context and nice look and feel.<br/>
							
							Hesitating? You should read <a href="/2011/01/04/springfuse-generates-primefaces-with-spring-webflow-frontend.html" target="_new">this blog (/w screenshots)</a>
							and eventually <a href="/jsf2-primefaces-spring-webflow-integration-tutorial.html" target="_new">JSF2/Primefaces/SpringWebflow</a> integration notes.
							</td></tr>
					<tr><td><input type="radio" name="frontEnd" id="springMvc" value="springMvc" class="updateCommand"></td>
						<td>Web application project using: <br/>Spring MVC 3, jQuery 1.5<br/>JPA 2 Entities/DAO/Service layers</td>
						<td>A classic web stack.<br/>
						Wondering how it looks? <a href="/2011/05/04/generate-spring-mvc3-jquery-jpa2-crud-applications.html" target="_new">Check this blog</a>.
						</td></tr>

					<tr><td><input type="radio" name="frontEnd"	 value="backendOnly" class="updateCommand"></td>
						<td>Backend only project using: <br/>JPA 2 Entities/DAO/Service layers</td>
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
		} else if (dbType == "db2") {
			if (urlDbType != "db2") {
				$("#jdbcUrl").val("jdbc:db2://localhost:50000/DBNAME");
			}
			$("#jdbcGroupId").val("com.ibm.db2");
			$("#jdbcArtifactId").val("db2jcc4");
			$("#jdbcDriver").val("com.ibm.db2.jcc.DB2Driver");
			$("#jdbcVersion").val("9.7.0.4");
		} else if (dbType == "mysql") {
			if (urlDbType != "mysql") {
				$("#jdbcUrl").val("jdbc:mysql://localhost/DBNAME");
			}
			$("#jdbcGroupId").val("mysql");
			$("#jdbcArtifactId").val("mysql-connector-java");
			$("#jdbcDriver").val("com.mysql.jdbc.Driver");
			$("#jdbcVersion").val("5.1.17");
		}

		if (dbType == "oracle") {
			$("#oracle-database").show();
		} else {
			$("#oracle-database").hide();
		}
		if (dbType == "db2") {
			$("#db2-database").show();
		} else {
			$("#db2-database").hide();
		}
		
		if (dbType == "other") {
			$("#other-database").show();
		} else {
			$("#other-database").hide();
		}
	}

	function param(key, value) {
                if (!value) {
                        value = "";
                }
		return "-D" + key + "=" + value.replace(/ /gi, "\\ ") + " ";
	}
	function isValidEmailAddress(emailAddress) {
		var pattern = new RegExp(/^(("[\w-\s]+")|([\w-]+(?:\.[\w-]+)*)|("[\w-\s]+")([\w-]+(?:\.[\w-]+)*))(@((?:[\w-]+\.)*\w[\w-]{0,66})\.([a-z]{2,6}(?:\.[a-z]{2})?)$)|(@\[?((25[0-5]\.|2[0-4][0-9]\.|1[0-9]{2}\.|[0-9]{1,2}\.))((25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1,2})\.){2}(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1,2})\]?$)/i);
		return pattern.test(emailAddress);
	}

	function updateCommand() {
		var version= "3.0.69";
		var groupId = $("#groupId").val();
		var artifactId = $("#artifactId").val();
		var email= $("#email").val();
		var frontEnd = $("input[name=frontEnd]:checked").val();
		var archetypeArtifactId = $("input[name=archetypeArtifactId]:checked").val();
		var proxyEnable = $("input[name=proxyEnable]:checked").val();

		$("#groupId").toggleClass("error", !groupId.match(/^([a-zA-Z]+){1}(\.[a-zA-Z0-9_]+)*$/));
		$("#artifactId").toggleClass("error", !artifactId.match(/^[a-zA-Z0-9]+$/));
		$("#email").toggleClass("error", email.length > 0 && !isValidEmailAddress(email));

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

		var cmd = 'mvn -U archetype:generate ';
		var cmd2 = '';
		cmd += param("archetypeGroupId", "com.springfuse.archetypes");
		cmd += param("archetypeArtifactId", archetypeArtifactId);
		cmd += param("archetypeVersion", version);
		cmd += param("groupId", groupId);
		cmd += param("package", groupId);
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
			$("#cmdLine").attr("rows", "12");
		} else {
			$("#cmdLine").attr("rows", "10");
		}
		cmd += param("interactiveMode", "false");
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
			cmd += param("proxyHost", proxyHost)
			cmd += param("proxyPort", proxyPort)
			if (proxyUsername) {
				cmd += param("proxyUsername", proxyUsername)
				cmd += param("proxyPassword", proxyPassword)
			}
			if (proxyNtlmDomain) {
				cmd += param("proxyNtlmEnable", "true")
				cmd += param("proxyNtlmDomain", proxyNtlmDomain)
				cmd += param("proxyNtlmWorkstation", proxyNtlmWorkstation)
			}
		}
		if(window.location.host.indexOf('localhost') != 0){
			cmd += param("archetypeRepository", "http://maven2.springfuse.com/")
		}
		cmd += "\n";
		cmd += 'cd ' + artifactId + '\n';
		if(window.location.host.indexOf('localhost') == 0){
			cmd2 = 'mvn -f springfuse.xml generate-sources -Dmaven-remote-generation-plugin.generationServiceLocation=http://localhost:9999/remote/generate\n';
		} else {
			cmd2 = 'mvn -f springfuse.xml generate-sources\n';
		}

		if (frontEnd !== "backendOnly") {
			$(".open-your-browser").show();
			cmd2 += 'mvn jetty:run\n';
		} else {
			$(".open-your-browser").hide();
			cmd2 += 'mvn install\n';
		}
		$("#cmdLine").val(cmd);
		$("#cmdLine2").val(cmd2);
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
		$("#cmdLine2").click(function() {
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

Once you are done, copy-paste sequentially these maven commands from step 2 and from step 4 in a console:

## Step 2/4: Bootstrap
Copy paste this first command in a console to create the minimal set of files required to reverse the database.
<textarea id="cmdLine" rows="4" cols="80" readonly="readonly" style="width:850px;height:85px; font-weight: bold" title="Cut and paste this command line to create your project"></textarea>

## Step 3/4:  Configuration (Optional)
Once you become familiar with Springfuse, you may want to <a href="/code-generation-configuration.html" target="_new">configure the code generation</a>.

## Step 4/4: Reverse and Code Generation

Copy paste these commands in a console to: 

* reverse your database schema, or the H2 database example we provide
* send the reversed database schema, not the data, to our server
* (generation duration depends on the number of tables)
* download the generated project from our server and unzip it.
* deploy the project locally using Jetty servlet container (<a href="http://localhost:8080/">http://localhost:8080/</a>) or, for backend project run all the unit tests.

<textarea id="cmdLine2" rows="2" cols="80" readonly="readonly" style="width:850px;height:40px;font-weight: bold"></textarea>

<p class="tip">
	If the remote generation fails (error, missing entities, etc.), please <a href="/faq.html#question_remote_generation_failed" target="_new">read this faq entry</a>.
	You should also provide a valid email in the form above to obtain the generation logs.
</p>

<p class="tip"> 
	The first time you use Springfuse or Maven you may be disappointed by the time Maven takes to download all the jar dependencies. Just be patient...
</p>

