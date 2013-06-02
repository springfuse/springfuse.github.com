---
layout: english
title: SpringFuse - Online Java Code Generator
---
<!-- Main hero unit for a primary marketing message or call to action -->
<div id="myCarousel" class="carousel slide hero-unit">
  <ol class="carousel-indicators">
    <li data-target="#myCarousel" data-slide-to="0" class="active"></li>
    <li data-target="#myCarousel" data-slide-to="1"></li>
    <li data-target="#myCarousel" data-slide-to="2"></li>
    <li data-target="#myCarousel" data-slide-to="3"></li>
  </ol>
  <!-- Carousel items -->
  <div class="carousel-inner">
    <div class="active item">
	    <h1>Springfuse <small>powered by celerio</small></h1>
		<h4>Code generator service for Java data-oriented applications</h4>
		<div class="carousel-caption">
			<p>&gt; Reverse your database schema</p>
			<p>&gt; Configure Springfuse and generate your project foundation</p>
			<p>&gt; Save weeks of R&amp;D in few seconds</p>
		</div>
    </div>
    <div class="item">
	    <h1>Springfuse <small>powered by celerio</small></h1>
		<h4>Stay ahead</h4>		
		<div class="carousel-caption">
			<p>&gt; Generated code follows recent industry standards</p>
			<p>&gt; 100% of generated code is already tested</p>
			<p>&gt; Generated code implements advanced features</p>
		</div>	
    </div>
    <div class="item">
	    <h1>Springfuse <small>powered by celerio</small></h1>
		<h4>Stay in control</h4>
	     <div class="carousel-caption">
			<p>&gt; The generated code is open</p>
			<p>&gt; Code quality fosters self-learning</p>
			<p>&gt; Springfuse is not present at runtime</p>
		</div>
    </div>
    <div class="item">
	    <h1>Springfuse <small>powered by celerio</small></h1>
		<h4>Boost your productivity</h4> 
		<div class="carousel-caption">
			<p>&gt; Focus your energy on business code right away</p>
			<p>&gt; Homogeneous technical code across projects</p>
			<p>&gt; Right to fail and retry</p>    
		</div>
    </div>
  </div>
  <!-- Carousel nav -->
  <a class="carousel-control left" href="#myCarousel" data-slide="prev">&lsaquo;</a>
  <a class="carousel-control right" href="#myCarousel" data-slide="next">&rsaquo;</a>
</div>
<script type="text/javascript">
$('.carousel').carousel({
  interval: 10000
});
</script>
<div>
	<p>
		<a href="https://github.com/jaxio/generated-projects" class="btn btn-primary">Review the code we generate</a>
		<a href="#gen" class="btn btn-primary">Generate an application now</a> | Current version: 3.0.101 | <a href="http://www.jaxio.com/documentation/celerio/change-log.html">Change Logs</a>
	</p>
</div>


## When to use Springfuse?

<a name="repet"></a>
### Eliminate repetitive tasks

When you identify a repetitive task, your duty is to automate it.
Springfuse automates the tedious and repetitive task of writing the first piece of code of a new Java project.

Actually this first piece of code that Springfuse generates constitute the backbone of your application. It goes way beyond a simple copy paste.
It covers subject such as persistence, 2d level cache, security, dependency injection, distribution, localization, unit tests, etc.

In just a few seconds, Springfuse relieves you from the burden of coding all this not-so-funny part of your application.

Therefore

* You save weeks.
* You reduce your risks.
* You learn from the generated code.
* You can focus on developing real features.
* You deliver on time.

### Learn faster technologies

There are so many Java technologies around! It is moving so fast!
Which ones to choose ? And then, what are the associated best practices ?
You do not always have the time to answer these questions.

Springfuse's mission is to deliver world-class project built on standard or de facto standard technologies following industry best practices

Therefore

* You reduce your maintenance costs.
* Developers learn faster and better with concrete code.
* You improve the overall quality of your project.

### Make it possible !

Cost cuttings, lack of resources, lack of training, impossible dead lines, you name it.

When the wall in front of you is too high, you just cannot climb it without help.
Springfuse can be a precious ladder. Here are two use cases:

### Prototyping

Writing a prototype for free is a common practice in the industry.
You have to work fast, for free, and deliver top notch quality to get the deal.

__Springfuse increases drastically your chances to succeed.__

### Application rewriting

Deciding to rewrite an application is a tough decision. 
There are often many risks.
However, when your customer ask for patches and features that you cannot deliver in time because of some some old code that nobody understand anymore, you do not have many choices. 
But it is too much work, you would need a second team, but there is no budget for that.

__Springfuse helps your existing team make the first move toward your application rewriting.__

<a name="gen"></a>
<br/><br/>
## Steps to generate a Java EE application

Before starting, if you are totally new to SpringFuse, you should take a few moment to <a href="/what-is-springfuse.html">understand how it works</a>.

__Requirements__

* Have at least Java 1.6 and Maven 2 installed on your machine.

<span class="label label-info">To generate a project</span>, adjust the settings below and execute the resulting command lines in a console.

### Step 1/4: Configure your project 

<form class="form-horizontal">

<div class="alert alert-info">
	Project informations
</div>

<!-- artifactId -->
<div class="control-group celerioVersion">
    <label class="control-label" for="celerioVersion">Celerio Version</label>
    <div class="controls">
		<select id="celerioVersion" name="celerioVersion" class="updateCommand">
			<option value="3.0.101">3.0.101</option>
			<option value="3.0.102-SNAPSHOT">3.0.102-SNAPSHOT</option>
		</select>    
		<span class="help-inline">The Celerio version that Springfuse should use</span>
	</div>
</div>

<!-- artifactId -->
<div class="control-group artifactId">
    <label class="control-label" for="artifactId">Project Name</label>
    <div class="controls">
		<input type="text" id="artifactId" value="myproject" placeholder="ex: myproject" class="required lettersNumbers updateCommand"/>
		<span class="help-inline">Use simple characters a-z, A-Z, 0-9, ex: myproject</span>
	</div>
</div>

<!-- groupId -->
<div class="control-group groupId">
    <label class="control-label" for="groupId">Java root package</label>
    <div class="controls">
		<input type="text" id="groupId" size="40" value="com.company.demo" placeholder="ex: com.jaxio.demo" class="required updateCommand" title="Ex: com.company.project"/>
    </div>
</div>

<!-- email -->
<div class="control-group email">
    <label class="control-label" for="email">Email</label>
    <div class="controls">
		<input type="text" id="email" class="required updateCommand"/>
		<span class="help-inline">It will be verified during the first generation process</span>
    </div>
</div>

<hr/>
<div class="control-group">
	<label class="control-label" for="frontEnd">Project type</label>
    <div class="controls">
      <label class="radio">
		<input type="radio" name="frontEnd" id="jsf2Spring" value="jsf2Spring" class="updateCommand" checked="checked"/>JSF 2, Primefaces 3.5, with conversation
			<span class="help-block">
				Ideal for enterprise data-oriented application requiring well organized code, conversation support, powerful features, nice look&amp;feel and development productivity.
				This is our favorite stack.
			</span>
	  </label>	  
      <label class="radio">
		<input type="radio" name="frontEnd" id="jsf2Simple" value="jsf2Simple" class="updateCommand" />JSF 2, Primefaces 3.5
			<span class="help-block">
				Same as above, without conversation... a bit simpler, but less powerful.
			</span>
	  </label>	  
      <label class="radio">
      <input type="radio" name="frontEnd" id="backendJpa" value="backendJpa" class="updateCommand"/>JPA 2 backend, with Query By Example feature
		<span class="help-block">      
      		Just the backend... Ideal if you want to develop your own front end stack or if you simply don't need one.
		</span>
      </label>
      <label class="radio">
		<input type="radio" name="frontEnd" id="jsf2Primefaces" value="jsf2Primefaces" class="updateCommand" />JSF 2, Primefaces 3.4 (Spring Web Flow 2.3.1)
			<span class="help-block">			
				This option is going to be removed in the coming months. We encourage you to use one of the options above.
			</span>		
	  </label>
    </div>
</div>

<div class="alert alert-info">
	Database settings
</div>

<!-- use example or reverse? -->
<div class="control-group">
	<label class="control-label" for="archetypeArtifactId3">Database to reverse</label>
    <div class="controls">
      <label class="radio">
			<input type="radio" name="archetypeArtifactId" id="archetypeArtifactId3" value="quickstart-embedded-db-with-configuration" class="updateCommand" checked="checked"/>Reverse a sample H2 database that we provide
	  </label>
      <label class="radio">
			<input type="radio" name="archetypeArtifactId" id="archetypeArtifactId1" value="quickstart" class="updateCommand"/>Reverse your own database			
      </label>
    </div>
</div>


<!-- dbType -->
<div class="jdbc-properties" style="display: none">
<p>
	<b>Database to reverse:</b>
</p>
<div class="control-group">
	<label class="control-label" for="dbType">Database Vendor</label>	
	<div class="controls">
		<select id="dbType" name="dbType" class="updateCommand">
			<option value="mysql">mysql</option>
			<option value="oracle">oracle</option>
			<option value="db2">db2</option>
			<option value="h2">h2</option>
			<option value="postgresql">postgresql</option>
			<option value="other">other</option>
		</select>
	</div>
</div>

<p>
	<b>Adjust the jdbc driver settings if needed:</b>
</p>

<div id="oracle-database" class="alert alert-warn" style="display: none">
	If you do not have an Oracle driver already in your maven repository please 
	<a href="/install-oracle-jdbc-driver-in-maven-repository.html" target="_new">install it manually</a>.
	<br/>
	If you rely on sequences to generate your PK ids, 
	you must configure Celerio during 'Step 3/4' below. Please refer to <a href="http://www.jaxio.com/documentation/celerio/configuration.html#seq_per_table" target="_new">'Use a SEQUENCE per TABLE'</a> 
</div>
<div id="db2-database" class="alert alert-warn" style="display: none">
	If you do not have an DB2 driver already in your maven repository please <a href="/reverse-db2-database-schema.html" target="_new">install it manually</a>.
</div>
<div id="other-database" class="alert alert-warn" style="display: none">
	Please replace the JDBC driver informations below with your own values.
</div>


<!-- jdbcGroupId -->
<div class="control-group">
	<label class="control-label" for="jdbcGroupId">Maven groupId</label>
    <div class="controls">
		<input type="text" name="jdbcGroupId" id="jdbcGroupId" class="updateCommand" placeholder="ex: mysql">
    </div>
</div>
	
<!-- jdbcArtifactId -->
<div class="control-group">
	<label class="control-label" for="jdbcArtifactId">Maven artifactId</label>
    <div class="controls">	
		<input type="text" name="jdbcArtifactId" id="jdbcArtifactId" class="updateCommand" placeholder="ex: mysql-connector-java"/>
	</div>		
</div>

<!-- jdbcGroupId -->
<div class="control-group">
	<label class="control-label" for="jdbcVersion">Version</label>
    <div class="controls">	
		<input type="text" name="jdbcVersion" id="jdbcVersion" class="updateCommand" placeholder="ex: 5.1.17"/>
	</div>
</div>	

<!-- jdbcDriver -->
<div class="control-group">
	<label class="control-label" for="jdbcDriver">Driver class</label>
    <div class="controls">
		<input type="text" name="jdbcDriver" id="jdbcDriver" class="updateCommand" placeholder="ex: com.mysql.jdbc.Driver"/>
	</div>
</div>

<p>
	<b>Now enter your database credentials.</b> Please do not use a production database.
</p>

<!-- jdbcUrl -->
<div class="control-group">
	<label class="control-label" for="jdbcUrl">Jdbc Url</label>
    <div class="controls">	
		<input type="text" name="jdbcUrl" id="jdbcUrl" class="updateCommand" placeholder="ex: jdbc:mysql://localhost/DBNAME"/>
	</div>
</div>

<!-- jdbcUser -->
<div class="control-group">
	<label class="control-label" for="jdbcUser">Db User</label>
    <div class="controls">
		<input type="text" name="jdbcUser" id="jdbcUser" class="updateCommand" placeholder="ex: user"/>
	</div>		
</div>

<!-- jdbcPassword -->
<div class="control-group">
	<label class="control-label" for="jdbcPassword">Db Password</label>
    <div class="controls">
		<input type="text" name="jdbcPassword" id="jdbcPassword" class="updateCommand" placeholder="ex: password"/>
	</div>		
</div>
</div>

<div class="alert alert-info">
	<i class="icon-wrench"> </i> Proxy Settings
</div>

<!-- proxyEnable ? -->
<div class="control-group">
	<label class="control-label" for="proxyEnable">Behind a proxy ?</label>
    <div class="controls">
      <label class="radio">
		<input type="radio" name="proxyEnable" id="proxyEnableFalse" value="false" class="updateCommand" checked="checked"/>No
	  </label>
      <label class="radio">
		<input type="radio" name="proxyEnable" id="proxyEnableTrue" value="true" class="updateCommand"/>Yes
      </label>
    </div>
</div>

<div class="proxy-properties" style="display: none">
	<p><b>Ok tell us more about your proxy:</b></p>

	<div class="control-group">
		<label class="control-label" for="proxyHost">Proxy hostname</label>
		<div class="controls">	
			<input type="text" name="proxyHost" id="proxyHost" class="updateCommand" value="intranet-proxy"/>
		</div>	
	</div>
	
	<div class="control-group">
		<label class="control-label" for="proxyPort">Proxy port</label>
		<div class="controls">	
			<input type="text" name="proxyPort" id="proxyPort" class="updateCommand" value="8080"/>
		</div>	
	</div>
	
	<div class="control-group">
		<label class="control-label" for="proxyUsername">Username</label>
		<div class="controls">	
			<input type="text" name="proxyUsername" id="proxyUsername" class="updateCommand" placeholder="ex: user"/>
		</div>	
	</div>
	
	<div class="control-group">
		<label class="control-label" for="proxyPassword">Password</label>
		<div class="controls">	
			<input type="password" name="proxyPassword" id="proxyPassword" class="updateCommand" placeholder="ex: password"/>
		</div>	
	</div>
	
	<div class="control-group">
		<label class="control-label" for="proxyNtlmDomain">Domain</label>
		<div class="controls">	
			<input type="text" name="proxyNtlmDomain" id="proxyNtlmDomain" class="updateCommand" placeholder="ex: mydomain"/>
			<span class="help-block">only if your proxy uses ntlm</span>
		</div>	
	</div>

	<div class="control-group">
		<label class="control-label" for="proxyNtlmWorkstation">Workstation</label>
		<div class="controls">	
			<input type="text" name="proxyNtlmWorkstation" id="proxyNtlmWorkstation" class="updateCommand" placeholder="ex: mymachine"/>
			<span class="help-block">only if your proxy uses ntlm
			<br/>
			Under Windows, 
				<ul>
					<li>Open System by clicking the Start button,</li>
					<li>click on Control Panel,</li>
					<li>click on System and Maintenance,</li>
					<li>click on System.</li>
				</ul>
				You can now find your computer's name.			
			</span>
		</div>
	</div>
	
	<div class="alert alert-warn">
		If not already done, please <a href="http://maven.apache.org/guides/mini/guide-proxies.html" target="_new">configure  maven to use this proxy</a> too.
	</div>	
</div>
</form>
<hr/>

Once you are <span class="label label-info">done</span>, copy-paste sequentially these maven commands from step 2 and from step 4 in a console:

### Step 2/4: Fetch the appropriate archetype

<p><span class="label label-info">Copy paste</span> the command below in a console to create the minimal set of files required to reverse the database.</p>

<textarea id="cmdLine" rows="6" cols="80" style="width:850px;height:80px;"></textarea>

### Step 3/4:  Configuration (Optional)

Once you <span class="label label-info">become familiar</span> with Springfuse, you may want to <a href="http://www.jaxio.com/documentation/celerio/configuration.html" target="_new">configure the code generation</a>.

### Step 4/4: Reverse and Code Generation

<span class="label label-info">Copy paste</span> these commands in a console to: 

* reverse your database schema, or the H2 database example we provide
* send only the database schema to our server
* download the generated project from our server and unzip it
* deploy the project locally using Jetty servlet container (<a href="http://localhost:8080/">http://localhost:8080/</a>) or, for backend project run all the unit tests.

<textarea id="cmdLine2" rows="2" cols="80" style="width:850px;height:40px;"></textarea>

<p class="tip">
	If the remote generation fails (error, missing entities, etc.), please <a href="/faq.html#question_remote_generation_failed" target="_new">read this faq entry</a>.
	You should also provide a valid email in the form above to obtain the generation logs.
</p>

<p class="tip"> 
	The first time you use Springfuse or Maven you may be disappointed by the time Maven takes to download all the jar dependencies. Just be patient...
</p>

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
			$("#jdbcVersion").val("1.3.171");
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
			$("#jdbcVersion").val("5.1.25");
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
		var version= $("#celerioVersion").val();
		var groupId = $("#groupId").val();
		var artifactId = $("#artifactId").val();
		var email= $("#email").val();
		var springData = $("input[name=springData]:checked").val();
		var frontEnd = $("input[name=frontEnd]:checked").val();
		var archetypeArtifactId = $("input[name=archetypeArtifactId]:checked").val();
		var proxyEnable = $("input[name=proxyEnable]:checked").val();

		if (springData) {
			frontEnd = frontEnd + "Sd";
		}

		$(".groupId").toggleClass("error", !groupId.match(/^([a-zA-Z]+){1}(\.[a-zA-Z0-9_]+)*$/));
		$(".artifactId").toggleClass("error", !artifactId.match(/^[a-zA-Z0-9]+$/));
		$(".email").toggleClass("error", email.length > 0 && !isValidEmailAddress(email));

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
		cmd += param("password", "none");

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

		if (frontEnd !== "backendJpa") {
			$(".open-your-browser").show();
		} else {
			$(".open-your-browser").hide();
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
