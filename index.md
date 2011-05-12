---
layout: main
title: Quickstart
---

# Quickstart

Springfuse reverses your database structure
and generates top-quality source code that you can use immediately as the foundation of your web application.
	
To generate a project, adjust the settings below and execute the resulting command lines in a console.

<div>	
	<form>
		<table>
			<tbody class="green-border">
				
				<tr>
					<th>Springfuse version</th>
					<td>
						<select id="version" class="required" class="updateCommand">
                            <option value="3.0.47" selected="selected">3.0.47</option>
						</select>
					</td>
				</tr>				
				<tr>
					<td colspan="2">
						<h2>Proxy Settings</h2>
					</td>
				</tr>
				<tr>
					<th>Http Proxy</th>
					<td>
						<table>
							<tbody>
								<tr>
									<td>
										Are you accessing this site through a http proxy?<br/>
										<input type="radio" name="proxyEnable" id="proxyEnableFalse" value="false" class="updateCommand" checked="checked"> No
										<input type="radio" name="proxyEnable" id="proxyEnableTrue" value="true" class="updateCommand"> Yes 									
                                                                        </td>
								</tr>
							</tbody>
						</table>
					</td>
				</tr>
				<tr class="proxy-properties" style="display: none">
					<th>Proxy settings</th>
					<td>
						<table>
							<tbody>
								<tr>
									<td colspan="2">
										You must configure both maven (<a target="_new"
											href="http://maven.apache.org/guides/mini/guide-proxies.html">instructions here</a>) and the springfuse maven plugin (fill the necessary fields below) to use your proxy.</p>
									</td>
								</tr>
								<tr>
									<th><label for="proxyHost" >proxy hostname</label></th>
									<td><input type="text" name="proxyHost" id="proxyHost" value="" size="40" class="updateCommand"></td>
								</tr>
								<tr>
									<th><label for="proxyPort" >proxy port</label></th>
									<td><input type="text" name="proxyPort" id="proxyPort" value="8080" size="6" class="updateCommand"></td>
								</tr>								
								<tr>
									<th><label for="proxyUsername">username</label></th>
									<td><input type="text" name="proxyUsername" id="proxyUsername" value="" class="updateCommand"></td>
								</tr>
								<tr>
									<th><label for="proxyPassword" >password</label></th>
									<td><input type="password" name="proxyPassword" id="proxyPassword" value="" class="updateCommand"></td>
								</tr>
								<tr>
									<th><label for="proxyNtlmDomain" >domain (only if your proxy uses ntlm)</label></th>
									<td><input type="text" name="proxyNtlmDomain" id="proxyNtlmDomain" value="" class="updateCommand"></td>
								</tr>
								<tr>
									<th><label for="proxyNtlmWorkstation" >workstation (only if your proxy uses ntlm)</label></th>
									<td><input type="text" name="proxyNtlmWorkstation" id="proxyNtlmWorkstation" value="" class="updateCommand"></td>
								</tr>
							</tbody>
						</table>
					</td>
				</tr>				
				<tr>
					<td colspan="2">
						<h2>Database Reverse Engineering Options</h2>
					</td>
				</tr>
				<tr>
					<th>DB Reverse Options</th>
					<td>
						<table>
							<tbody>
								<tr>
									<th><input type="radio" name="archetypeArtifactId" id="archetypeArtifactId3" value="quickstart-embedded-db-with-configuration" class="updateCommand" checked="checked"></th>
									<td><label for="archetypeArtifactId3" title="No need to have a database, <br/>we will create an embedded database for you, and reverse it">Reverse a sample H2 database that we provide</label></td>
								</tr>
								<tr>
									<th><input type="radio" name="archetypeArtifactId" id="archetypeArtifactId1" value="quickstart" class="updateCommand"></th>
									<td><label for="archetypeArtifactId1" title="You just need to provide some basic info so our plugin can reverse your database. <br/> do not try this with production database, use your development database.">Reverse your own database</label></td>
								</tr>
							</tbody>
						</table>					
					</td>
				</tr>
				<tr class="jdbc-properties" style="display: none">
					<th>JDBC Driver<br/>(Maven dependency)</th>
					<td>
						<table>
							<tbody>
								<tr>
									<td colspan="2">
										Which JDBC driver should springfuse plugin use to access your database ?				
									</td>
								</tr>							
								<tr>
									<th><label for="dbType">Database Vendor</label></th>
									<td>
										<select id="dbType" name="dbType" class="updateCommand">
											<option value="mysql">mysql</option>
											<option value="oracle">oracle</option>
											<option value="h2">h2</option>
											<option value="postgresql">postgresql</option>
											<option value="other">other</option>
										</select>
										<p id="oracle-database" style="display: none" class="important">
											<a href="/install-oracle-jdbc-driver-in-maven-repository">You must install and configure your Oracle JDBC driver first</a>
										</p>											
									</td>
								</tr>
								<tr>
									<th><label for="jdbcGroupId">maven groupId</label></th>
									<td><input type="text" name="jdbcGroupId" id="jdbcGroupId" value="" class="updateCommand"></td>
								</tr>
								<tr>
									<th><label for="jdbcArtifactId">maven artifactId</label></th>
									<td><input type="text" name="jdbcArtifactId" id="jdbcArtifactId" value="" class="updateCommand"></td>
								</tr>
								<tr>
									<th><label for="jdbcGroupId" >version</label></th>
									<td><input type="text" name="jdbcVersion" id="jdbcVersion" value="" class="updateCommand"></td>
								</tr>
								<tr>
									<th><label for="jdbcDriver">driver class</label></th>
									<td><input type="text" name="jdbcDriver" id="jdbcDriver" value="" class="updateCommand"></td>
								</tr>
							</tbody>
						</table>
					</td>
				</tr>				
				<tr class="jdbc-properties"  style="display: none">
					<th>Jdbc connectivity</th>
					<td>
						<table>
							<tbody class="no-border">
								<tr>
									<td colspan="2">
										Please provide your database credentials so the springfuse plugin can connect to your database and reverse it.<br/>
										<p class="important">
										DO NOT provide here your production database credentials. You should only reverse a database used for development.
										</p>
										These settings will be used as well in the generated project to access your database.
									</td>
								</tr>							
								<tr>
									<th><label for="jdbcUrl">url</label></th>
									<td><input type="text" name="jdbcUrl" id="jdbcUrl" value="" size="40" class="updateCommand"></td>
								</tr>
								<tr>
									<th><label for="jdbcUser">User</label></th>
									<td><input type="text" name="jdbcUser" id="jdbcUser" value="" class="updateCommand"></td>
								</tr>
								<tr>
									<th><label for="jdbcPassword" >Password</label></th>
									<td><input type="text" name="jdbcPassword" id="jdbcPassword" value="" class="updateCommand"></td>
								</tr>
							</tbody>
						</table>
					</td>
				</tr>
				<tr>
					<td colspan="2">
						<h2>Code Generation Options</h2>
					</td>
				</tr>				
				<tr>
					<th>Your project Java root package</th>
					<td>
						<input type="text" id="groupId" size="40" value="com.company.project" class="required packageName updateCommand">
					</td>
				</tr>
				<tr>
					<th>Project name</th>
					<td>
						<input type="text" id="artifactId" value="myproject" class="required lettersNumbers updateCommand">
					</td>
				</tr>
				<tr>
					<th>Front end technology</th>
					<td>
						<select id="frontEnd" class="required" class="updateCommand">
                            <option value="jsf2Primefaces" selected="selected">JSF2 + PrimeFaces + Spring WebFlow</option>
                            <option value="springMvc">Spring MVC + JQuery</option>
							<option value="backendOnly">None, generate only the backend: JPA2 Entities, DAOs, etc.</option>
						</select>
					</td>
				</tr>
				<tr>
					<th>Advanced Configuration</th>
					<td>
						<p>Once you get familiar with the generation process, 
						   you can refer to <a href="/code-generation-configuration">Code Generation Configuration</a> to control more precisely the code generation.</p>
					</td>
				</tr>				
				<tr>
					<td colspan="2">
						<h2>Maven Command to Execute</h2>
					</td>								
				<tr>
					<td colspan="2">
					    <p>Once you are done, copy-paste these maven commands lines in a console:</p>
						<textarea id="cmdLine" rows="3" cols="80" readonly="readonly" style="width:850px;height:110px" title="Cut and paste this command line to create your project"></textarea>
						<p class="open-your-browser">
							Then once all is ready you can open your browser and go to <a href="http://localhost:8080/">http://localhost:8080/</a>
						</p>
						<p class="tip">
							If the remote generation fails (error, missing entities, etc.), please <a href="/faq#question_remote_generation_failed">read this faq entry</a>.
						</p>					
					</td>
				</tr>
			</tbody>
		</table>
	</form>
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
				cmd += 'mvn generate-sources -Dmaven-remote-generation-plugin.generationServiceLocation=http://'+$(location).attr('host')+'/remote/generate\n';
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

## Requirements
* Java Development Kit 1.6
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
