# How to fasten your integrations with custom built cache

## The problem

My customer had a tough requirement to query, process and visualise data for end users in their UI. The data fetched to UI via Scripted Rest API. It queries and processes a big bunch of data, and the calculation is slow, which then results to subpar user experience for the user interacting with the component.

This is something that wouldn't be an issue, if ServiceNow would have a built in cache functionality to custom APIs. It's a reasonable wish to have, ServiceNow has done it elsewhere (__remote tables__). 

## Solution = Build Your Own Cache!

Create a table with fields:
* Response
* Path
* QueryParams
* PathParams
* Created on (will be included as a default)

Create new class (=Script Include), **cacheUtils**, with functions **getRecentResultIfExist** and **insertResponseToCache**.

In Scripted Rest API's resources, modify the script to something like below:

    var cacheUtils = new cacheUtils();
	var recentResultIfExist = cacheUtils.getRecentResultIfExist(qParamsObj,pathParamsObj,request.uri);
	if (recentResultIfExist) return recentResultIfExist;

	var responseCalculationUtils = new heavyCalculationScriptInclude();
    var result = responseCalculationUtils.doHeavyCalculation(whatEverParams);
	cacheUtils.insertResponseToCache(result,qParamsObj,pathParamsObj,request.uri);
    return result;

Also, be sure to define flushing logic for the cache. No need to store records for a longer period of time. Simplest way to implement it is via **sys_auto_flush**.

When you are writing the functions, utilise JSON.parse and JSON.stringify functions to convert request parameters to valid query strings and back. The actual cacheUtils implementation might look something like this:

	var CacheUtils = Class.create();
	CacheUtils.prototype = {
		initialize: function() {
		},

		getRecentResultIfExist: function(qParamsObj,pathParamsObj,path) {
			var grCache = new GlideRecord(CACHE_TABLE);
			grCache.addQuery('query_parameters',JSON.stringify(qParamsObj));
			grCache.addQuery('path_parameters',JSON.stringify(pathParamsObj));
			grCache.addQuery('sys_created_on','>', gs.minutesAgo(10));
			grCache.addQuery('path',path);
			grCache.orderByDesc('sys_created_on');
			grCache.setLimit(1);
			grCache.query();
			if (grCache.next()) {
				return JSON.parse(grCache.response);
			} 
			else return undefined;
		},


		insertResponseToCache: function (responseObj,qParamsObj,pathParamsObj,path) {
			var grCache = new GlideRecord(CACHE_TABLE);
			grCache.query_parameters = JSON.stringify(qParamsObj);
			grCache.path_parameters = JSON.stringify(pathParamsObj);
			grCache.response = JSON.stringify(responseObj);
			grCache.path = path;
			grCache.insert();

		},

		type: 'CacheUtils'
	};

## Result
Response time improved ~98%, from 5000ms to 100ms.

 ![Graph](https://raw.githubusercontent.com/artturipa/myblog/main/rest_cache/cahcegraph.png)

