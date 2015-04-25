---
title: Azure AppService Hands-On Lab
layout: default
---

# AppService Hands-On Lab

In this lab...

First you will create both a new mobile app backend and a simple *To do list* app that stores app data in the new mobile app backend. The mobile app backend uses the supported .NET languages for server-side business logic. The client app can use any client platform supported by Mobile App, including iOS, Windows, Xamarin iOS, and Xamarin Android.

Then, you will create a web app, using the same database as your mobile app. At the end of the tutorial, you will have a web client and a mobile client that work with the same data.

>If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](http://go.microsoft.com/fwlink/?LinkId=523751), where you can immediately create a short-lived starter web app in App Service. No credit cards required; no commitments.

## Table of Contents

1. [Create a new mobile app backend](create-a-new-mobile-app-backend)
2. [Create a new universal Windows app](create-a-new-universal-windows-app)
3. [Connect an AngularJS Web Client to the Mobile App](connect-an-angularjs-web-client-to-the-mobile-app)
4. [Create API App with ASP.NET Web API](create-an-api-app-wtih-aspnet-web-api)
5. [Create a Logic App](create-a-logic-app)

## Prerequisites

1. [Microsoft Azure Subscription](http://azure.microsoft.com/en-us/pricing/free-trial/)
2. [Visual Studio Community Edition](http://go.microsoft.com/?linkid=9863608)
3. [Visual Studio 2013 Update 4](https://www.microsoft.com/en-us/download/details.aspx?id=44921)
4. [Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)

## Create a new mobile app backend

{% include 01-01-01-AppServiceHOL/app-service-mobile-dotnet-backend-create-new-service-preview.md %}

## Create a new universal Windows app

{% include 01-01-01-AppServiceHOL/app-service-mobile-universal-windows-client.md %}

## Connect an Angular Web Client to the Mobile App

{% include 01-01-01-AppServiceHOL/app-service-web-angular-web-client-mobile-app-api.md %}

## Create an API App with ASP.NET Web API

{% include 01-01-01-AppServiceHOL/app-service-api-create-api-app.md %}

## Create a Logic App

{% include 01-01-01-AppServiceHOL/app-service-logic-create-logic-app.md %}