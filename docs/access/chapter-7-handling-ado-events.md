---
title: "Chapter 7 Handling ADO Events"
  
  
manager: soliver
ms.date: 11/16/2014
ms.audience: Developer
 
  
localization_priority: Normal
ms.assetid: 22924fe2-d00d-8a0c-52f5-2dc6039537ff
description: "The ADO event model supports certain synchronous and asynchronous ADO operations that issue events , or notifications, before the operation starts or after it completes. An event is actually a call to an event-handler routine that you define in your application."
---

# Chapter 7: Handling ADO Events

The ADO event model supports certain synchronous and asynchronous ADO operations that issue  *events*  , or notifications, before the operation starts or after it completes. An event is actually a call to an event-handler routine that you define in your application. 
  
If you provide handler functions or procedures for the group of events that occur before the operation starts, you can examine or modify the parameters that were passed to the operation. Because it has not been executed yet, you can either cancel the operation or allow it to complete.
  
The group of events that occur after an operation completes are especially important if you use ADO asynchronously. For example, an application that starts an asynchronous [Recordset.Open](open-method-ado-recordset.md) operation is notified by an execution complete event when the operation concludes. 
  
Using the ADO event model adds some overhead to your application but provides far more flexibility than other methods of dealing with asynchronous operations, such as monitoring the [State](state-property-ado.md) property of an object with a loop. 
  
