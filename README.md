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
* Make it so that unchecking the catering checkbox clears the other order.
* Update the workflow to have better approval flow.
* Remove Quanitity if catering is chosen.
* Add a when option to ordering your sub.

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

##Usage

>To use the item simply go to the service catalog, and select Services. The subs ordering menu will appear as one of the options with a Sub picture beside it.
![image](https://user-images.githubusercontent.com/80430334/127918620-a2be3cbf-a721-4f0f-8eed-d25db7fae91e.png)
After clicking the option you have two choices: ordering catering, or ordering a sub. Multiple subs can be ordered, but catering can only choose on option from several variables with additional options added. Clicking "Add" on ordering your sub allows you to choose which bread and ingredients you want in the sub and autopopulates your name.
![image](https://user-images.githubusercontent.com/80430334/127919700-88dc7d92-b48e-4ab6-832e-a3eeab2eddec.png)
If you choose catering you get several option for choosing what you want to be catered as well as options for the catering: tea dispenser, provided seating. You also fill out the address, date, and time of the event.
![image](https://user-images.githubusercontent.com/80430334/127920083-ba04ab01-42d1-4aee-bd37-af4a93573315.png)
After clicking order it will be in the hands of the "Sandwich Artists" and you will get a stage summary to look at.
![image](https://user-images.githubusercontent.com/80430334/127920285-f6153b7a-2bef-4826-aa30-269410e821f1.png)
If you chose to order a sub you would go to get it when it is ready, and if you chose catering you would wait until the time arrives, unless the request is rejected for improper timing.

## Contributors
>Nicolas E. Bauer
