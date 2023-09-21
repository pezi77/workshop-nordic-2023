Extending Content Types
========================
When you develop a new software, you almost always start with analyzing the domain model. The same is true for the CoreMedia CMS - as the domain model is the source for modeling the content type model. The content type model is the backbone of the CoreMedia CMS as it describes what content means to you. Basically, there are two places within the Blueprint workspace you may use when you define your own content type model or extend the one in the Blueprint. You will get to know both of them by defining a new content type CMHelloWorld as a child of CMTeaser within a new file mydoctypes.xml. The file has the following structure:

<?xml version="1.0" encoding="ISO-8859-1" ?>
<DocumentTypeModel
  xmlns="http://www.coremedia.com/2008/documenttypes"
  Name="my-doctypes">

 <ImportGrammar Name="coremedia-richtext-1.0"/>
 <ImportDocType Name="CMTeaser"/>

 <DocType Name="CMHelloWorld" Parent="CMTeaser">
   <StringProperty Name="message" Length="32"/>
 </DocType>
</DocumentTypeModel>
XML
Defining content types in contentserver-blueprint-component

The first and a little easier way of defining CMHelloWorld is to put the new file mydoctypes.xml into the directory apps/content-server/modules/server/contentserver-blueprint-component/src/main/resources/framework/doctypes/my/. To create a subfolder under doctypes for your customization, in this example named "my", is a good option.

After doing so, you can test your new content type. To do so, you have to build the contentserver-blueprint-component module, and the content-server-app module as follows. Remember to stop the server if you have not done it already.

$ cd apps/content-server/modules/server/contentserver-blueprint-component
$ mvn clean install
$ cd ../../../spring-boot/content-server-app
$ mvn clean install
BASH
Now, start the Content Management Server application and take a look into its log file. You should see the following message, telling you that the Content Server created a new database table for the new content type.

[INFO]  SQLStore - DocumentTypeRegistry: creating table:
CREATE TABLE CMHelloWorld( id_ INT NOT NULL, version_ INT NOT NULL,
isApproved_ TINYINT, isPublished_ TINYINT, editorId_ INT,
approverId_ INT, publisherId_ INT, editionDate_ DATETIME,
approvalDate_ DATETIME, publicationDate_ DATETIME,
"locale" VARCHAR(32), "masterVersion" INT, "keywords" VARCHAR(1024),
"validFrom" DATETIME, "validFrom_tz" VARCHAR(30), "validTo" DATETIME,
"validTo_tz" VARCHAR(30), "segment" VARCHAR(64), "title" VARCHAR(512),
"teaserTitle" VARCHAR(512), "notSearchable" INT, "message" VARCHAR(32),
PRIMARY KEY (id_, version_),  FOREIGN KEY (id_) REFERENCES Resources(id_))
PLAIN TEXT
Using a Separate Module in the Context of an Extension

The second option is the more flexible way. You build your own module in the context of an extension. The following steps require an existing extension module my-extension. Proceed as follows:

Create a new subfolder my-extension-server in the apps/content-server/modules/extensions/my-extension directory.

Create a pom.xml file and add the following contents.:

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>com.coremedia.blueprint</groupId>
    <artifactId>my-extension</artifactId>
    <version>${project.version}</version>
    <relativePath>../pom.xml</relativePath>
  </parent>

  <artifactId>my-extension-server</artifactId>

  <properties>
    <coremedia.project.extension.for>
      server
    </coremedia.project.extension.for>
  </properties>

</project>
XML
Adjust the groupId and artifactId of the parent declaration according to your project settings.

Add this module’s Maven coordinates to the extension descriptor of the extension.

Create the subfolder src/main/resources/framework/doctypes/myextension.

Copy the content type definition file mydoctypes.xml into the folder created in the last step.

Enable the extension as desribed in Project Extensions.

Further Reading
Learn more about the syntax of content type definitions: Developing a Content Type Model

Learn how to update a content type schema: Schema Update

Learn more about CoreMedia extensions: Project Extensions
