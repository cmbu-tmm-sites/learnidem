---
title: "Basic Commands"
weight: 40
---

<SPAN STYLE="font-size:18.0pt">STATES</SPAN><br>
Idem states are used to make sure resources are in a desired state. The desired state of a resource can be specified in sls file. 

 <ul>
<li><p><b>Present State</b></p> 
    makes sure a resource exists in a desired state. If a resource does not exist, running present will create the resource on the provider. If a resource exists, running present will update the resource on the provider. (Only the values that the Cloud Provider REST API supports can be updated.)</li>
<li><p><b>Absent State</b></p>
    makes sure a resource does not exist. If a resource exits, running absent will delete the resource. If a resource does not exist, running absent is a no-operation.</li>
<li><p><b>Describe State</b></p>
    lists all the current resources of the same resource type under the <b>subscription id</b> specified in the credential profile.</li>
 </ul>


