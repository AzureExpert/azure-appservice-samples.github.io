### Enable CORS in Mobile App

{% include 01-01-01-AppServiceHOL/task-enable-cors.md %}

### Create Angular Web Client

1. In Visual Studio, right-click on the Solution, Click **Add > New Project...** 
2. Select **ASP.NET Web Application**
3. Name the Project `webHOL`
4. In the New ASP.NET Project Dialogue select the **Empty** template
5. Create a new folder to the project called **App**
6. Create a new file in the App folder called **index.html**

	```
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <title>MultiChannel ToDo</title>
	    <meta name="viewport" content="width=device-width, initial-scale=1">
	    <link href="lib/bootstrap/css/bootstrap.min.css" rel="stylesheet" />
	    <link href="lib/bootstrap/css/bootstrap-theme.min.css" rel="stylesheet" />
	    <link href="css/site.css" rel="stylesheet" />
	</head>
	
	<body ng-app="multiChannelToDo">
	
	    <div class="container" ng-controller="ToDoController">
	        <h1><span class="glyphicon glyphicon-list-alt"></span> To Do List</h1>
	        <div class="check-list-container">
	            <div class="check-list-item-container">
	                <ul class="check-list">
	                    <li id="check-list-item-{{item.id}}" ng-repeat="item in items" ng-hide="{{item.complete}}" ng-click="complete(item)" class="check-list-item"><span class="glyphicon glyphicon-check" aria-hidden="true"></span> {{item.text}} - {{item.phoneNumber}}</li>
	                </ul>
	            </div>
	        </div>
	        <hr class=""/>
	        <div class="controls-container">
	            <form ng-submit="add()" class="form-inline">
	                <div class="form-group">
	                    <input id="Text" ng-model="itemText" type="text" class="form-control" placeholder="Task" />
	                    <input id="PhoneNumber" ng-model="itemPhone" type="tel" class="form-control" placeholder="Phone Number" />
	                    <button class="btn btn-primary">Add Item</button>
	                </div>
	            </form>
	        </div>
	    </div>
	
	    <script src="lib/jquery/jquery.min.js" type="text/javascript"></script>
	    <script src="lib/angular/angular.min.js" type="text/javascript"></script>
	    <script src="lib/bootstrap/js/bootstrap.min.js" type="text/javascript"></script>
	    <!-- AngularJS App -->
	    <script src="js/app.js" type="text/javascript"></script>
	    <script src="js/controllers/ToDoController.js" type="text/javascript"></script>
	    <script src="js/services/ToDoService.js" type="text/javascript"></script>
	
	</body>
	</html>
	```

7. create a new file in the App folder called **web.config**
	
	```
	<?xml version="1.0" encoding="utf-8"?>
	<!--
	  For more information on how to configure your ASP.NET application, please visit
	  http://go.microsoft.com/fwlink/?LinkId=169433
	  -->
	<configuration>
	  <system.web>
	    <compilation debug="true" targetFramework="4.5" />
	    <httpRuntime targetFramework="4.5" />
	  </system.web>
	  <appSettings>
	    <add key="apiPath" value=""/>
	  </appSettings>
	  <system.webServer>
	    <staticContent>
	      <mimeMap fileExtension="eot" mimeType="application/vnd.ms-fontobject" />
	      <mimeMap fileExtension="ttf" mimeType="application/octet-stream" />
	      <mimeMap fileExtension="woff" mimeType="font/x-woff" />
	      <mimeMap fileExtension="woff2" mimeType="font/x-woff2" />
	      <mimeMap fileExtension="json" mimeType="application/json"/>
	    </staticContent>
	  </system.webServer>
	</configuration>

	```

6. Create three (3) folders in App called **css**, **js**, and **lib**
7. Create a new file in the css folder called **site.css** and paste the following:

	```
	.container {
	    width: 300px;
	    margin: auto;
	    margin-top: 60px;
	    padding: 10px;
	}
	
	ul.check-list {
	    -webkit-padding-start: 0px;
	}
	
	div.check-list-container {
	    width: 300px;
	    min-height: 200px;
	    text-align: right;
	}
	
	li.check-list-item {
	    height: 40px;
	    width: 225px;
	    padding-bottom: 2px;
	    list-style-type: none;
	    text-align: left;
	}
	
	    li.check-list-item span.glyphicon {
	        padding: 10px;
	    }
	
	div.controls-container {
	    text-align: right;
	}

	```
	
8. Create a new file in the js folder called **app.js**

	```
	var multiChannelToDoApp = angular.module('multiChannelToDo', []);
	var apiPath = "http://mobilehol-code.azurewebsites.net/tables";
	```

9. Create two (2) folders in the js folder called **controllers** and **services**
10. Create a new file in the controllers folder called **ToDoController.js**

	```
	'use strict';
	multiChannelToDoApp
	    .controller('ToDoController', ['$scope', 'toDoService', function ($scope, toDoService) {
	
	        $scope.get = function () {
	            toDoService.getItems()
	                .success(function (data) {
	                    $scope.items = data;
	            });
	        };
	
	        $scope.add = function () {
	            toDoService.add($scope.itemText, $scope.itemPhone)
	            .success(function(data){
	                $scope.itemText = '';
	                $scope.itemPhone = '';
	                $scope.get();
	            });
	        };
	
	        $scope.complete = function (item) {
	            toDoService.complete(item)
	                .success(function (data) {
	                    $scope.get();
	                });
	        };
	
	        $scope.get();
	
	}]);
	```

11. Create a new file in the services folder called **ToDoService.js**

	```
	'use strict';
	multiChannelToDoApp
	    .factory('toDoService', ['$http', function ($http) {
	        return {
	
	            getItems: function () {
	                return $http.get(apiPath + '/TodoItem');
	            },
	
	            add: function (task, phoneNumber) {
	                return $http.post(apiPath + '/TodoItem', { "text": task, "phoneNumber": phoneNumber, "complete": false });
	            },
	
	            complete: function (item) {
	                return $http.patch(apiPath + '/TodoItem/' + item.id, { "id": item.id, "text": item.text, "complete": true });
	            }
	        }
	    }]);
	```

12. Create three (3) folders in the lib folder called **angular**, **bootstrap**, **jquery**
13. Download the minified Angular library from [code.angularjs.org](https://code.angularjs.org/1.3.6/angular.min.js)
14. Download the bootstrap library from [getbootstrap.com](https://github.com/twbs/bootstrap/releases/download/v3.3.2/bootstrap-3.3.2-dist.zip)
15. Download the minified jquery library from [jquery.com](http://code.jquery.com/jquery-2.1.3.min.js)