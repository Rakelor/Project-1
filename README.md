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
* Notifications will be sent out to employees assigned to dealing with creating the subs and delivering

To-do list:
* Make it so that the requestor gets a notification that their order was rejected due to improper timing, etc.
* Re-work the workflow to make it so that it is only activated during proper times.
* Update the workflow to have better approval flow.

## Getting Started

(Ensure that the two tables Breads and Ingredients are created and populated)
(Create the users that are to deal with the approvals and tasks as well as assign roles)
(Create the Catalog Item and create a variable checkbox, and two variable sets)

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
