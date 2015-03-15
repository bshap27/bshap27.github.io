---
layout: post
title: Rails Generators Cheat Sheet
---

Rails generators are pure magic: we use them to create the basic framework for our rails apps so that we don't have to undergo the tedious exercise of creating the structure ourselves. There are 5 basic commands we use quite frequently that fall at various levels of abstraction. We choose to use one over the other depending on the level of complexity our models require. Although there are plenty of resources online that document rails generators and how to use them, I I couldn't find a single consolidated cheat sheet anywhere on the web. I've created a chart below that has already mitigated some of the confusion for me, so I wanted to share it with you, dear reader.

In order of abstraction from least to greatest the commands rank as follows:
<ol>
	<li class='override_list'>rails generate migration</li>
	<li class='override_list'>rails generate model</li>
	<li class='override_list'>rails generate controller</li>
	<li class='override_list'>rails generate resource</li>
	<li class='override_list'>rails generate scaffold</li>
</ol>

And the table below documents what you can expect to be created for you when you use each one:
<table style="width:100%">
  <tr>
    <th> Command </th>
    <th width=15%> Syntax: Model name + ? </th>
    <th> Model </th>
    <th> Migration </th>
    <th> Controller </th>
    <th> Views </th>
    <th> Test Suite </th>
    <th> Assets (Javascripts, Stylesheets) </th>
    <th> Route in config file </th>
    <th> Helper </th>
  </tr>
  <tr>
    <td>Migration</td>
    <td>attributes as name:type</td> 
    <td>N</td>
    <td>Y</td>
    <td>N</td>
    <td>N</td>
    <td>N</td>
    <td>N</td>
    <td>N</td>
    <td>N</td>
  </tr>
  <tr>
    <td>Model</td>
    <td>attributes as name:type</td> 
    <td>Y</td>
    <td>Y</td>
    <td>N</td>
    <td>N</td>
    <td>model</td>
    <td>N</td>
    <td>N</td>
    <td>N</td>
  </tr>
  <tr>
    <td>Controller</td>
    <td>views</td> 
    <td>N</td>
    <td>N</td>
    <td>Y</td>
    <td>Y</td>
    <td>controller</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
  </tr>
  <tr>
    <td>Resource</td>
    <td>attributes as name:type</td>  
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td>folder; no files</td>
    <td>controller, model</td>
    <td>Y</td>
    <td>N</td>
    <td>Y</td>
  </tr>
  <tr>
    <td>Scaffold</td>
    <td>attributes as name:type</td>  
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td>controller, model</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
  </tr>
</table>

<p>Don't forget, if you ever choose the wrong one and want to undo, you can use the rails destroy command. For example, if you created a scaffold for Becca but realized you only needed a controller, you could execute:</p>
<code>rails destroy scaffold becca<br>
rails generate controller becca index show</code>

Just remember that it will remove any and all files related to your Becca model, so use with caution.

:)