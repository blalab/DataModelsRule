# Rule
Spin a full featured back-end (database, search engine, RESTful API, back-end UI, logging, email communication, user management, etc) with no more than a configuration file (the Data Model).

####Motivation
Data Models have existed forever. Everybody knows they are necessary but almost all the time they just don't exist in a real project. It is as if everybody wants to just start coding and creating databases and indexes. After months of development,  the closest thing we get is somebody printing the schema of the database in the command line (if a relational db is being used) or showing you the ORM class for some implementation that already exists. 

Rule flips the whole process. You focus in the DataModel and Rule builds the application for you. 

####Idea
What if the Data Model existed in an agnostic configuration file (YAML or JSON or any other similar) and the Database, API, Backend and Fronted where ruled by it. That is, the Data Model being the absolute single source of truth ... period.

Wouldn't it be cool to open the DataModel file add/remove an entity or field and by act of magic have the database, api, backend and fronted morph into that?

Wouldn't it be nice to open source that one DataModel file for a whole community to decide what fields to be added, what to be deprecated, etc? You feel like you are going in another direction? No problem, just fork it (the data model) and feed it to Rule for it to cook your new application.

This is different than having to follow a predefined standard schema defined by a superior body and their lenghty proposals and working groups. This is just you spining a model in 15 minutes and running it in your application. You'll be entering data and displaying it in your frontend by lunch.

Analyze this. Since you are no longer hard-coding anything you are no longer coupled to a version of your db,  api or frontend. Even more, you could offer a different version to every user (or group of users), you would just need to point their session to a different datamodel file.

Ok, too much daydreaming. Lets build this:

###Quickstart

This is a JSON file that describes the types and its characteristics. 

Lets say you want to create an application for a Bicycle museum. The curator tells you the bicycle with the following fields: Model, Manufacturer, Year, Color, Image(s), URL to its official website, Fixed Gear (True/False).

The main entity is Bicycle. however there are other entities like Manufacturer , Bicycle colors that you need to also model. If you are lucky enough you might find a native type that already offers something you need (like Year)

```
{
  types:[
    {
    "Name":"bicycle"
    "fields":[
      {
       "Name":"Model",
       "Widget":"text",
      },
      {
       "Name":"Manufacturer",
       "Widget":"select",
       "Source":{"type":"manufacturer"}
      },
      {
       "Name":"Year",
       "Widget":"select",
       "Source":{"type":"year"}
      },
      {
       "Name":"Color",
       "Widget":"select",
       "Source":{"type":"bicycle-colors"}
      },
      {
       "Name":"Catalog Images",
       "Widget":"image",
       "Cardinality":"multiple"
      },
      {
       "Name":"Official Website",
       "Widget":"URL"
      },
      {
       "Name":"Other references",
       "Widget":"URL",
       "Cardinality":"multiple"
      },
      {
       "Name":"Fixed gear?",
       "Widget":"checkbox"
      }
    },
    {
    "Name": "Manufacturer"
    },
    {
    "Name": "Bicycle Color"
    }
  ]
}
```

