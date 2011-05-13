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
</style>
<table id="quickstart">
	<tbody>
		<tr>
			<th>Project</th>
			<td>
				<table>
					<tbody>
						<tr>
							<th style="width:120px;">Name</th>
							<td><input type="text" id="artifactId" value="myproject" class="required lettersNumbers updateCommand"></td>
						</tr>
						<tr>
							<th style="width:120px;">Root package</th>
							<td><input type="text" id="groupId" size="40" value="com.company.project" class="required packageName updateCommand" title="Ex: com.company.project"></td>
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
							<td><input type="text" name="jdbcUrl" id="jdbcUrl" value="" size="70" class="updateCommand"></td>
						</tr>
						<tr>
							<th><label for="jdbcUser">User</label></th>
							<td><input type="text" name="jdbcUser" id="jdbcUser" value="" class="updateCommand"></td>
						</tr>
						<tr>
							<th><label for="jdbcPassword">Password</label></th>
							<td><input type="text" name="jdbcPassword" id="jdbcPassword" value="" class="updateCommand"></td>
						</tr>
					</tbody>
				</table>
				<p class="important">
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
									If you do not have an Oracle driver already in your maven repository please <a href="/install-oracle-jdbc-driver-in-maven-repository">install it manually</a>.
								</span>
							</td>
						</tr>
						<tr>
							<th><label for="jdbcGroupId">Maven groupId</label></th>
							<td><input type="text" name="jdbcGroupId" id="jdbcGroupId" value="" size="50" class="updateCommand"></td>
						</tr>
						<tr>
							<th><label for="jdbcArtifactId">Maven artifactId</label></th>
							<td><input type="text" name="jdbcArtifactId" id="jdbcArtifactId" value="" size="50" class="updateCommand"></td>
						</tr>
						<tr>
							<th><label for="jdbcGroupId">Version</label></th>
							<td><input type="text" name="jdbcVersion" id="jdbcVersion" value="" class="updateCommand"></td>
						</tr>
						<tr>
							<th><label for="jdbcDriver">Driver class</label></th>
							<td><input type="text" name="jdbcDriver" id="jdbcDriver" value="" size="50" class="updateCommand"></td>
						</tr>
					</tbody>
				</table>
			</td>
		</tr>
		<tr>
			<th>Generate</th>
			<td>
				<input type="radio" name="frontEnd" id="backendOnly" value="backendOnly" class="updateCommand">
				<label for="springMvc" title="You have the basics, all the tables will have a domain object generated, and the jpa setup is done etc.<br/>
												Use this option if you are new to Springfuse or java.">
					Maven 3 + Java entities + Spring 3 + JPA 2 + Spring Security 3
				</label>
				<br/>
				<input type="radio" name="frontEnd" id="springMvc" value="springMvc" class="updateCommand">
				<label for="springMvc" title="You have an out-of-the box working web application running spring mvc with the latest best practices.">
					Maven 3 + Java entities + Spring 3 + JPA 2 + Spring Security 3 + Spring MVC 3 + JQuery 1.5
				</label>
				<br/>
				<input type="radio" name="frontEnd" id="jsf2Primefaces" value="jsf2Primefaces" class="updateCommand" checked="checked">
				<label for="jsf2Primefaces" title="Many enterprise applications have complex navigation and requirements.<br/>
													For these type of applications MVC is too low level, JSF and Weflow are the way to go.<br/>
													But these technologies are complex to master, use this generation option to learn how to set them up.">
					Maven 3 + Java entities + Spring 3 + JPA 2 + Spring Security 3 + JSF 2 + PrimeFaces 2.2 + Spring WebFlow 3
				</label>
			</td>
		</tr>
		<tr>
			<th>Http Proxy</th>
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
								<td><input type="text" name="proxyHost" id="proxyHost" value="" size="50" class="updateCommand"></td>
							</tr>
							<tr>
								<th><label for="proxyPort">Proxy port</label></th>
								<td><input type="text" name="proxyPort" id="proxyPort" value="8080" size="6" class="updateCommand"></td>
							</tr>
							<tr>
								<th><label for="proxyUsername">Username</label></th>
								<td><input type="text" name="proxyUsername" id="proxyUsername" value="" class="updateCommand"></td>
							</tr>
							<tr>
								<th><label for="proxyPassword">Password</label></th>
								<td><input type="password" name="proxyPassword" id="proxyPassword" value="" class="updateCommand"></td>
							</tr>
							<tr>
								<th><label for="proxyNtlmDomain">Domain</label></th>
								<td>
									<input type="text" name="proxyNtlmDomain" id="proxyNtlmDomain" value="" class="updateCommand">
									<i>only if your proxy uses ntlm</i>
								</td>
							</tr>
							<tr>
								<th><label for="proxyNtlmWorkstation">Workstation</label></th>
								<td>
									<input type="text" name="proxyNtlmWorkstation" id="proxyNtlmWorkstation" value="" class="updateCommand">
									<i>only if your proxy uses ntlm</i>
								</td>
							</tr>
						</tbody>
					</table>
					<p class="important">
						If not already done, please <a href="http://maven.apache.org/guides/mini/guide-proxies.html">configure  maven to use this proxy</a> too.
					</p>
				</div>
			</td>
		</tr>
		<tr>
			<th>Advanced Configuration</th>
			<td>
				Once you get familiar with the generation process, please refer to the <a href="/code-generation-configuration">code generation configuration</a> documentation to control more precisely the code generation.<br/>
			</td>
		</tr>
		<tr>
			<th><i>Your email</i></th>
			<td>
				<input type="text" id="email" value="" class="updateCommand" title="Used to send you personnalized tips, in case of generation failure for example."> <i>optional</i>
			</td>
		</tr>
	</tbody>
</table>
<script type="text/javascript">
	function updateDbTypeDefaultValues() {
		var dbType = $("#dbType").val();

		if (dbType == "h2") {
			$("#jdbcUrl").val("jdbc:h2:~/.h2/DBNAME");
			$("#jdbcGroupId").val("com.h2database");
			$("#jdbcArtifactId").val("h2");
			$("#jdbcDriver").val("org.h2.Driver");
			$("#jdbcVersion").val("1.2.131");
		} else if (dbType == "postgresql") {
			$("#jdbcUrl").val("jdbc:postgresql://localhost/DBNAME");
			$("#jdbcGroupId").val("postgresql");
			$("#jdbcArtifactId").val("postgresql");
			$("#jdbcDriver").val("org.postgresql.Driver");
			$("#jdbcVersion").val("8.2-504.jdbc3");
		} else if (dbType == "oracle") {
			$("#jdbcUrl").val("jdbc:oracle:thin:@localhost:1521:XE");
			$("#jdbcGroupId").val("com.oracle");
			$("#jdbcArtifactId").val("ojdbc14");
			$("#jdbcDriver").val("oracle.jdbc.driver.OracleDriver");
			$("#jdbcVersion").val("10.2.0.3");
		} else if (dbType == "mysql") {
			$("#jdbcUrl").val("jdbc:mysql://localhost/DBNAME");
			$("#jdbcGroupId").val("mysql");
			$("#jdbcArtifactId").val("mysql-connector-java");
			$("#jdbcDriver").val("com.mysql.jdbc.Driver");
			$("#jdbcVersion").val("5.1.6");
		} else {
			$("#jdbcUrl").val("");
			$("#jdbcGroupId").val("");
			$("#jdbcArtifactId").val("");
			$("#jdbcDriver").val("");
			$("#jdbcVersion").val("");
		}

		if (dbType == "oracle") {
			$("#oracle-database").show();
			
		} else {
			$("#oracle-database").hide();
		}
	}

	function updateCommand() {
		var groupId = $("#groupId").val();
		var artifactId = $("#artifactId").val();
		var version= $("#version").val();
		var email= $("#email").val();
		var frontEnd= $("#frontEnd").val();
		var archetypeArtifactId = $("input[name=archetypeArtifactId]:checked").val();
		var proxyEnable = $("input[name=proxyEnable]:checked").val();

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
		cmd += '-DarchetypeGroupId=com.springfuse.archetypes ';
		cmd += '-DarchetypeArtifactId=' + archetypeArtifactId + ' ';
		cmd += '-DarchetypeVersion=' + version + ' ';
		cmd += '-DgroupId=' + groupId + ' ';
		cmd += '-Dpackage=' + groupId + ' ';
		cmd += '-DartifactId=' + artifactId + ' ';
		cmd += '-Dversion=1.0.0 ';
		cmd += '-DfrontEnd=' + frontEnd + ' ';
		cmd += '-Demail=' + email + ' ';
		
		if(window.location.host.indexOf('localhost') == -1){
			cmd += '-DarchetypeRepository=http://maven2.springfuse.com/ ';
		}
		if (archetypeArtifactId == "quickstart") {
			cmd += '-DjdbcGroupId=' + $("#jdbcGroupId").val() + " ";
			cmd += '-DjdbcArtifactId=' + $("#jdbcArtifactId").val() + " ";
			cmd += '-DjdbcVersion=' + $("#jdbcVersion").val() + " ";
			cmd += '-DjdbcDriver=' + $("#jdbcDriver").val() + " ";
			cmd += '-DjdbcUser=' + $("#jdbcUser").val() + " ";
			cmd += '-DjdbcPassword=' + $("#jdbcPassword").val() + " ";
			cmd += '-DjdbcUrl=' + $("#jdbcUrl").val() + " ";
			$("#cmdLine").attr("rows", "14");
		} else {
			$("#cmdLine").attr("rows", "12");
		}
		cmd += '-DinteractiveMode=false ';
		
		var proxyHost = $("#proxyHost").val();
		var proxyPort = $("#proxyPort").val();
		var proxyUsername= $("#proxyUsername").val();
		var proxyPassword= $("#proxyPassword").val();
		var proxyNtlmDomain= $("#proxyNtlmDomain").val();
		var proxyNtlmWorkstation= $("#proxyNtlmWorkstation").val();

		if (proxyEnable === "true" && proxyHost) {
			cmd += "-DproxyEnable=true ";
			cmd += "-DproxyHost=" + proxyHost + " ";
			cmd += "-DproxyPort=" + proxyPort + " ";

			if (proxyUsername) {
				cmd += "-DproxyUsername=" + proxyUsername + " ";
				cmd += "-DproxyPassword=" + proxyPassword + " ";
			}

			if (proxyNtlmDomain) {
				cmd += "-DproxyNtlmEnable=true ";
				cmd += "-DproxyNtlmDomain=" + proxyNtlmDomain + " ";
				cmd += "-DproxyNtlmWorkstation=" + proxyNtlmWorkstation + " ";
			}
		}

		cmd += "\n";
		
		cmd += 'cd ' + artifactId + '\n';
		if(window.location.host.indexOf('localhost') == 0){
			cmd += 'mvn generate-sources -Dmaven-remote-generation-plugin.generationServiceLocation=http://' + window.location.host + '/remote/generate\n';
		} else {
			cmd += 'mvn generate-sources\n';
		}
		
		cmd += 'cd ..\n';
		cmd += 'cd ' + artifactId + '-generated\n';
		if (frontEnd !== "backendOnly") {
			$(".open-your-browser").show();
			cmd += 'mvn jetty:run\n';
		} else {
			$(".open-your-browser").hide();
			cmd += 'mvn install\n';
		}
		$("#cmdLine").val(cmd);
		$(".project-name").html(artifactId);
	}
	
	$(document).ready(function() {
		$(".updateCommand").change(updateCommand);
		$("#cmdLine").click(function() {
			$(this).select();
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
<textarea id="cmdLine" rows="6" cols="80" readonly="readonly" style="width:850px;height:130px" title="Cut and paste this command line to create your project"></textarea>
<p class="open-your-browser">
	Then once all is ready you can open your browser and go to <a href="http://localhost:8080/">http://localhost:8080/</a>
</p>
<p class="tip">
	If the remote generation fails (error, missing entities, etc.), please <a href="/faq#question_remote_generation_failed">read this faq entry</a>.
</p>

## Requirements

* JDK 1.6
* Maven 2 at least.

<p class="tip"> 
The first time you use Springfuse or Maven you may be disappointed by the time it takes to download all the jar dependencies. Just be patient...
</p>

## How It Works

Filling the form below allows you to prepare few Maven 2 commands that ultimately run your generated project!

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

<p class="important">
Do not import the intermediary project in your IDE. Instead, import the generated project, 
its folder name ends with '-generated'.
</p>

