# Subs Your Way

## Project Description
The project creates a catalog item, as well as a few tables and a workflow to create a Sub ordering service, and puts it into the catalog services.

## Technologies Used

* ServiceNow Platform
* UI Policies and Client Script Includes
* Workflow

## Features

List of the features ready and TODOs for future Development
* Able to choose between Catering and simple ordering without seeing each other at the same time.
![image](https://user-images.githubusercontent.com/80430334/127917767-e887fd53-31b4-4fb3-a91c-1d1e82feb3df.png)
![image](https://user-images.githubusercontent.com/80430334/127917787-a3757eb9-bda2-4efb-be55-9b9fd0d536ed.png)
* Notifications and tasks will be sent out to employees assigned to dealing with creating the subs and delivering
* ![image](https://user-images.githubusercontent.com/80430334/127918083-706bee6d-c497-4f07-aa0a-8aaf4bf662b0.png)


To-do list:
* Make it so that the requestor gets a notification that their order was rejected due to improper timing, etc.
* Re-work the workflow to make it so that it is only activated during proper times.
* Update the workflow to have better approval flow.

## Getting Started

(Ensure that the two tables Breads and Ingredients are created and populated)
![image](https://user-images.githubusercontent.com/80430334/127918168-f6d2f230-3050-4bc9-9359-7f02cbed69a0.png)
![image](https://user-images.githubusercontent.com/80430334/127918192-a683e7be-a744-4647-8b16-fd8785344832.png)
(Create the users that are to deal with the approvals and tasks as well as assign roles)
![image](https://user-images.githubusercontent.com/80430334/127918251-d814460d-2765-44f9-ad06-014d0aa17675.png)
(Create the Catalog Item and create a variable checkbox, and two variable sets)
![image](https://user-images.githubusercontent.com/80430334/127918322-092c1ead-f607-4870-89cd-839e1cc5a653.png)
![image](https://user-images.githubusercontent.com/80430334/127918343-ce344a30-251d-416a-93c7-834735fb3aa2.png)

- Script Includes code: 
var requestor_details = Class.create();
requestor_details.prototype = Object.extendsObject(AbstractAjaxProcessor, {
 requestor_info: function() {


  var result = this.newItem("result");


  var logged_user = gs.getUserID();


  var user_detail = new GlideRecord('sys_user');


  user_detail.addQuery('sys_id',logged_user);


  user_detail.query();


  while(user_detail.next())


  {

  result.setAttribute("user",user_detail.sys_id);

  }


  },


    type: 'requestor_details'
});

![image](https://user-images.githubusercontent.com/80430334/127917183-3283fdc1-1f99-4863-9c8a-374fbe1c2f87.png)

-Variable Set Code: 
function onLoad() {
   var ga = new GlideAjax("requestor_details");


  ga.addParam("sysparm_name","requestor_info");


  ga.getXML(ajaxResponse);


  function ajaxResponse(serverResponse) {


  var result = serverResponse.responseXML.getElementsByTagName("result");


  var user = result[0].getAttribute("user");

  g_form.setValue('name',user);


}
}
![image](https://user-images.githubusercontent.com/80430334/127917131-aabaa354-02b2-4eb9-972d-7ce81469e446.png)
