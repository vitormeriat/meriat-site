---
layout: post
title: Meu guia de estudos para o Exam 70-487 Developing Windows Azure and Web Services
date: 2013-12-27 16:21:32.000000000 -02:00
type: post
published: true
status: publish
categories:
- Certification
- Microsoft Azure
- Services

---
<p align="justify"><a href="http://blob.vitormeriat.com.br/images/2013/12/lrg.jpg"><img title="lrg" style="border-top:0;border-right:0;background-image:none;border-bottom:0;float:left;padding-top:0;padding-left:0;margin:0 25px 0 0;border-left:0;display:inline;padding-right:0;"   alt="lrg" src="http://blob.vitormeriat.com.br/images/lrg.jpg" width="160" align="left" height="191" /></a>Olá pessoal, estou compilando aqui todo o material que utilizei para me preparar para este exame. Para quem ainda não sabe o Training Kit deste exame só esteve previsto para vendas apartir do fim de Novembro. Como não quis esperar tive de iniciar os estudos por conta própria, o que me rendeu uma porção de anotações que devo transformar em posts além de um gua que vou compartilhar com vocês. Este post trata-se apenas uma junção de conteúdos e referências, algumas sugeridas em outros blogs e que estou compilando aqui. </p>
<p><!--more-->
<p align="justify">Como fiz a prova hoje posso ir adiantando que algumas partes em que esperava maior dificuldade me deparei com questões simples, onde a experiência de trabalho já dá um bom ganho. A maior difuldade do teste esteve nos Esutudos de Casos onde a questão está inserida em um determinado contexto… No mais segue o guia de estudos e os sites de referência no fim do post.</p>
<p>&#160;</p>
<h2><b>Accessing Data (24%)</b></h2>
<p><i></i></p>
<h3><i><font style="font-weight:bold;">Choose data access technologies</font></i></h3>
<p align="justify">This objective may include but is not limited to: Choose a technology (ADO.NET, Entity Framework, WCF Data Services) based on application requirements</p>
<ul>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/cc668792.aspx">WCF Data Services</a>, <a href="http://msdn.microsoft.com/en-us/library/cc668794.aspx">WCF Data Services Overview</a>, and <a href="http://msdn.microsoft.com/en-us/library/cc668810.aspx">WCF Data Services | Getting Started</a> (covers&#160; “WCF Data Services” overview)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/data/jj590134">Introducing Entity Framework</a>, <a href="http://msdn.microsoft.com/en-us/library/bb399567.aspx">Entity Framework Overview</a>, &amp; <a href="http://msdn.microsoft.com/data/ee712907">Entity Framework | Get Started</a> (covers “Entity Framework” overview)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/h43ks021.aspx">ADO.NET Overview</a> (covers “ADO.NET” overview)</div>
</li>
</ul>
<h3 align="justify"><i><font style="font-weight:bold;">Implement caching</font></i></h3>
<p align="justify">This objective may include but is not limited to: Cache static data, apply cache policy (including expirations); Use CacheDependency to refresh cache data; query notifications</p>
<ul>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/75xawe1d.aspx">SqlCacheDependency Class</a> (covers “Use CacheDependency to refresh cache data”, “Cache static data, apply cache policy (including expirations)” sections)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/xfs0kkt8.aspx">SqlCacheDependencyAdmin Class</a> (covers “query notifications” section)</div>
</li>
</ul>
<h3 align="justify"><i><font style="font-weight:bold;">Implement transactions</font></i></h3>
<p align="justify">This objective may include but is not limited to: manage transactions by using the API from System.Transactions namespace; implement distributed transactions; specify transaction isolation level</p>
<ul>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/a90c30fy.aspx">System.Transactions</a> (covers “manage transactions by using the API from System.Transactions namespace” section)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/ms254973.aspx">Distributed Transactions</a> and <a href="http://msdn.microsoft.com/en-us/library/h5w5se33.aspx">TransactionScope Class</a> (covers “implement distributed transactions” sections)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/system.transactions.transaction.isolationlevel.aspx">IsolationLevel Property</a> and <a href="http://msdn.microsoft.com/en-us/library/system.transactions.isolationlevel.aspx">IsolationLevel Enumeration</a> (covers “specify transaction isolation level” section)</div>
</li>
<li>
<div align="justify">System.Transactions namespace (<a href="http://msdn.microsoft.com/en-us/library/system.transactions.aspx">http://msdn.microsoft.com/en-us/library/system.transactions.aspx</a>)</div>
</li>
</ul>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/clip_image002.png"><img title="clip_image002" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="clip_image002" src="http://blob.vitormeriat.com.br/images/clip_image002.png" width="560" height="442" /></a></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/clip_image004.png"><img title="clip_image004" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="clip_image004" src="http://blob.vitormeriat.com.br/images/clip_image004.png" width="560" height="392" /></a></p>
<h3><i><font style="font-weight:bold;"></font></i></h3>
<h3 align="justify"><i><font style="font-weight:bold;">Implement data storage in Windows Azure</font></i></h3>
<ul>
<li>
<div align="justify">When to use blob, tables, queues, sql db (see <b>Data management</b> section on <a href="http://pluralsight.com/training/Courses/TableOfContents/azure-bigpicture">http://pluralsight.com/training/Courses/TableOfContents/azure-bigpicture</a>)</div>
</li>
<li>
<div align="justify">Azure caching (<a href="http://pluralsight.com/training/courses/TableOfContents?courseName=azure-caching">http://pluralsight.com/training/courses/TableOfContents?courseName=azure-caching</a>)</div>
</li>
<li>
<div align="justify">XPath and LINQ to XML (LINQ to XML section on <a href="http://pluralsight.com/training/courses/TableOfContents?courseName=linq-data-access">http://pluralsight.com/training/courses/TableOfContents?courseName=linq-data-access</a>)</div>
</li>
</ul>
<p align="justify">This objective may include but is not limited to: access data storage in Windows Azure; Choose data storage mechanism in Windows Azure (blobs, tables, queues, SQL Database); Distribute data by using the Content delivery network (CDN); Handle exceptions by using retries (SQL Database); manage Windows Azure Caching</p>
<ul>
<li>
<div align="justify"><a href="http://social.technet.microsoft.com/wiki/contents/articles/1674.data-storage-offerings-on-the-windows-azure-platform.aspx">Data Storage Offerings on the Windows Azure Platform</a> (covers “Choose data storage mechanism in Windows Azure (blobs, tables, queues, SQL Database)” section)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/gg433040.aspx">Blobs, Queues, and Tables</a> (covers “access data storage in Windows Azure” section)</div>
</li>
<li>
<div align="justify"><a href="http://www.windowsazure.com/en-us/develop/net/common-tasks/cdn/">Using Windows Azure CDN - .NET – Develop</a> (covers “Distribute data by using the Content delivery network (CDN)” section)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/windowsazure/gg278356.aspx">Caching in Windows Azure</a> (covers “manage Windows Azure Caching” section)</div>
</li>
<li>
<div align="justify"><a href="http://social.technet.microsoft.com/wiki/contents/articles/4235.retry-logic-for-transient-failures-in-windows-azure-sql-database-en-us.aspx">Retry Logic for Transient Failures in Windows Azure SQL Database</a> and <a href="http://code.msdn.microsoft.com/windowsazure/SQL-Azure-Retry-Logic-2d0a8401">SQL Azure Retry Logic sample in C# for Visual Studio 2010</a> (covers “Handle exceptions by using retries (SQL Database)” section)</div>
</li>
<li>
<div align="justify">Azure CDN (<a href="http://www.windowsazure.com/en-us/develop/net/common-tasks/cdn/?redirectToLocale=false">http://www.windowsazure.com/en-us/develop/net/common-tasks/cdn/?redirectToLocale=false</a> and <a href="http://www.windowsazure.com/en-us/develop/net/fundamentals/intro-to-windows-azure/#caching">http://www.windowsazure.com/en-us/develop/net/fundamentals/intro-to-windows-azure/#caching</a>)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/pt-br/windowsazure/hh500327">Blob (PT-BR)</a></div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/pt-br/windowsazure/hh500332">Tables (PT-BR)</a></div>
</li>
</ul>
<h3 align="justify"><i><font style="font-weight:bold;"></font></i></h3>
<h3 align="justify"><i><font style="font-weight:bold;">Create and implement a WCF Data Services service</font></i></h3>
<p align="justify">This objective may include but is not limited to: Address resources; implement filtering; create a query expression; access payload formats (including JSON); use data service interceptors and service operators</p>
<ul>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/data/odata.aspx">WCF Data Services</a> (overview)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/data/gg601462">Building an OData Service (Part I)</a> (covers “Address resources”, “implement filtering” sections)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/data/gg591296">Consuming OData using .NET</a> (covers “create a query expression” section)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/data/gg617675">Consuming OData using jQuery</a> (covers “access payload formats (including JSON) ” section)</div>
</li>
</ul>
<h3 align="justify"><font style="font-weight:bold;"></font></h3>
<h3 align="justify"><font style="font-weight:bold;">Filters Examples</font></h3>
<ul>
<li>
<div align="justify">Retrieve All Customers <a href="http://localhost:65363/NorthwindService.svc/Customers">http://localhost:65363/NorthwindService.svc/Customers</a></div>
</li>
<li>
<div align="justify">Retrieve All Products <a href="http://localhost:65363/NorthwindService.svc/Products">http://localhost:65363/NorthwindService.svc/Products</a></div>
</li>
<li>
<div align="justify">Retrieve the Customer Whose CustomerID (primary key) is WOLZA <a href="http://localhost:65363/NorthwindService.svc/Customers('WOLZA')">http://localhost:65363/NorthwindService.svc/Customers('WOLZA')</a></div>
</li>
<li>
<div align="justify">Retrieve the Products Whose ProductID (primary key) is 10 <a href="http://localhost:65363/NorthwindService.svc/Products(10)">http://localhost:65363/NorthwindService.svc/Products(10)</a></div>
</li>
<li>
<div align="justify">Retrieve the CompanyName from the Customer Whose CustomerID (primary key) is QUICK <a href="http://localhost:57087/NorthwindService.svc/Customers('QUICK')/CompanyName">http://localhost:57087/NorthwindService.svc/Customers('QUICK')/CompanyName</a></div>
</li>
<li>
<div align="justify">Retrieve the Orders (navigation property) for the Customer Whose CustomerID (primary key) is QUICK <a href="http://localhost:57087/NorthwindService.svc/Customers('QUICK')/Orders">http://localhost:57087/NorthwindService.svc/Customers('QUICK')/Orders</a></div>
</li>
<li>
<div align="justify">Retrieve the Supplier’s CompanyName from the Supplier (navigation property) of Product 1 (primary Key) <a href="http://localhost:57087/NorthwindService.svc/Products(1)/Supplier/CompanyName">http://localhost:57087/NorthwindService.svc/Products(1)/Supplier/CompanyName</a></div>
</li>
<li>
<div align="justify">Retrieve the Count of Orders for the Customer Whose CustomerID (primary key) is QUICK <a href="http://localhost:57087/NorthwindService.svc/Customers('QUICK')/Orders/$count">http://localhost:57087/NorthwindService.svc/Customers('QUICK')/Orders/$count</a></div>
</li>
<li>
<div align="justify">Retrieve the CompanyName Value from the Customer Whose CustomerID (primary key) is QUICK <a href="http://localhost:57087/NorthwindService.svc/Customers('QUICK')/CompanyName/$value">http://localhost:57087/NorthwindService.svc/Customers('QUICK')/CompanyName/$value</a></div>
</li>
<li>
<div align="justify">Retrieve the ProductID, ProductName, and UnitPrice for the Product Whose ProductID is 1(primary key) <a href="http://localhost:57087/NorthwindService.svc/Products(1)?$select=ProductID,ProductName,UnitPrice">http://localhost:57087/NorthwindService.svc/Products(1)?$select=ProductID,ProductName,UnitPrice</a></div>
</li>
<li>
<div align="justify">Retrieve the CustomerID and CompanyName for all Customers <a href="http://localhost:57087/NorthwindService.svc/Customers?$select=CustomerID,CompanyName">http://localhost:57087/NorthwindService.svc/Customers?$select=CustomerID,CompanyName</a></div>
</li>
<li>
<div align="justify">Retrieve Customers Ordered By ContactName <a href="http://localhost:57087/NorthwindService.svc/Customers?$orderby=ContactName">http://localhost:57087/NorthwindService.svc/Customers?$orderby=ContactName</a></div>
</li>
<li>
<div align="justify">Retrieve Employees Ordered By LastName, FirstName <a href="http://localhost:57087/NorthwindService.svc/Employees?$orderby=LastName,FirstName">http://localhost:57087/NorthwindService.svc/Employees?$orderby=LastName,FirstName</a></div>
</li>
<li>
<div align="justify">Retrieve Products Ordered By UnitPrice Descending <a href="http://localhost:57087/NorthwindService.svc/Products?$orderby=UnitPrice">http://localhost:57087/NorthwindService.svc/Products?$orderby=UnitPrice</a> desc</div>
</li>
<li>
<div align="justify">Retrieve First 3 Customers <a href="http://localhost:57087/NorthwindService.svc/Customers?$top=3">http://localhost:57087/NorthwindService.svc/Customers?$top=3</a></div>
</li>
<li>
<div align="justify">Retrieve Top 3 of Highest Priced Products <a href="http://localhost:57087/NorthwindService.svc/Products?$orderby=UnitPrice">http://localhost:57087/NorthwindService.svc/Products?$orderby=UnitPrice</a> desc&amp;$top=3</div>
</li>
<li>
<div align="justify">Retrieve 3 Customers after Skipping 18 Customers <a href="http://localhost:57087/NorthwindService.svc/Customers?$orderby=CustomerID&amp;$skip=18&amp;$top=3">http://localhost:57087/NorthwindService.svc/Customers?$orderby=CustomerID&amp;$skip=18&amp;$top=3</a></div>
</li>
<li>
<div align="justify">Retrieve Products Whose Unit Price Is Greater than 10 <a href="http://localhost:65363/NorthwindService.svc/Products?$filter=UnitPrice">http://localhost:65363/NorthwindService.svc/Products?$filter=UnitPrice</a> gt 10</div>
</li>
<li>
<div align="justify">Retrieve Orders Where the CustomerID Equals ALFKI <a href="http://localhost:65363/NorthwindService.svc/Orders?$filter=CustomerID">http://localhost:65363/NorthwindService.svc/Orders?$filter=CustomerID</a> eq 'ALFKI'</div>
</li>
<li>
<div align="justify">Retrieve Products Whose UnitsInStock Is Less than or Equal to 2 <a href="http://localhost:65363/NorthwindService.svc/Products?$filter=UnitsInStock">http://localhost:65363/NorthwindService.svc/Products?$filter=UnitsInStock</a> le 2</div>
</li>
<li>
<div align="justify">Retrieve Discontinued Product Whose UnitPrice Is Greater than or Equal to 50 <a href="http://localhost:65363/NorthwindService.svc/Products?$filter=Discontinued">http://localhost:65363/NorthwindService.svc/Products?$filter=Discontinued</a> eq true and UnitPrice ge 50</div>
</li>
<li>
<div align="justify">Retrieve Products Whose ProductName Starts with C <a href="http://localhost:65363/NorthwindService.svc/Products?$filter=startswith(ProductName,'C')">http://localhost:65363/NorthwindService.svc/Products?$filter=startswith(ProductName,'C')</a></div>
</li>
<li>
<div align="justify">Retrieve Customers Whose CompanyName Contains restaurant <a href="http://localhost:65363/NorthwindService.svc/Customers?$filter=substringof('restaurant',CompanyName)">http://localhost:65363/NorthwindService.svc/Customers?$filter=substringof('restaurant',CompanyName)</a></div>
</li>
<li>
<div align="justify">Retrieve Orders Placed in 1998 <a href="http://localhost:65363/NorthwindService.svc/Orders?$filter=year(OrderDate)">http://localhost:65363/NorthwindService.svc/Orders?$filter=year(OrderDate)</a> eq 1998</div>
</li>
<li>
<div align="justify">Retrieve Orders Placed in February of 1998 <a href="http://localhost:65363/NorthwindService.svc/Orders?$filter=year(OrderDate)">http://localhost:65363/NorthwindService.svc/Orders?$filter=year(OrderDate)</a> eq 1998 and month(OrderDate) eq 2</div>
</li>
<li>
<div align="justify">Retrieve Products Whose UnitPrice Floor Is 19 <a href="http://localhost:65363/NorthwindService.svc/Products?$filter=floor(UnitPrice)">http://localhost:65363/NorthwindService.svc/Products?$filter=floor(UnitPrice)</a> eq 19</div>
</li>
<li>
<div align="justify">Retrieve Products Whose UnitPrice Rounds to 29 <a href="http://localhost:65363/NorthwindService.svc/Products?$filter=round(UnitPrice)">http://localhost:65363/NorthwindService.svc/Products?$filter=round(UnitPrice)</a> eq 29</div>
</li>
<li>
<div align="justify">Retrieve Products Whose UnitPrice Ends with .5 <a href="http://localhost:65363/NorthwindService.svc/Products?$filter=UnitPrice">http://localhost:65363/NorthwindService.svc/Products?$filter=UnitPrice</a> sub floor(UnitPrice) eq 0.5</div>
</li>
<li>
<div align="justify">Retrieve the Customer Whose CustomerID Is QUICK and the Orders for QUICK <a href="http://localhost:57087/NorthwindService.svc/Customers('QUICK')?$expand=Orders">http://localhost:57087/NorthwindService.svc/Customers('QUICK')?$expand=Orders</a></div>
</li>
<li>
<div align="justify">Retrieve the Customer Whose CustomerID Is ALFKI and the Orders and Order_Details for ALFKI <a href="http://localhost:57087/NorthwindService.svc/Customers('ALFKI')?$expand=Orders/Order_Details">http://localhost:57087/NorthwindService.svc/Customers('ALFKI')?$expand=Orders/Order_Details</a></div>
</li>
</ul>
<h3 align="justify"><i><font style="font-weight:bold;"></font></i></h3>
<h3 align="justify"><i><font style="font-weight:bold;">Manipulate XML data structures</font></i></h3>
<p align="justify">This objective may include but is not limited to: Read, filter, create, modify XML data structures; Manipulate XML data by using XMLReader, XMLWriter, XMLDocument, XPath, LINQ to XML; transform XML by using XSLT transformations</p>
<ul>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/system.xml.xmlnode.aspx">XmlNode Class (System.Xml)</a> and <a href="http://msdn.microsoft.com/en-us/library/system.xml.xmldocument%28v=vs.71%29.aspx">XmlDocument Class</a> (covers “Read, filter, create, modify XML data structures” section)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/system.xml.xmlwriter.aspx">XmlWriter Class (System.Xml)</a>, <a href="http://msdn.microsoft.com/en-us/library/system.xml.xmlreader.aspx">XmlReader Class (System.Xml)</a>, <a href="http://msdn.microsoft.com/en-us/library/system.xml.xmldocument%28v=vs.71%29.aspx">XmlDocument Class</a>, <a href="http://msdn.microsoft.com/en-us/library/system.xml.xmlnode.aspx">XmlNode Class (System.Xml)</a>, and <a href="http://msdn.microsoft.com/en-us/library/system.xml.xpath.xpathnavigator.aspx">XPathNavigator Class (System.Xml.XPath)</a> (covers “Manipulate XML data by using XMLReader, XMLWriter, XMLDocument, XPath” section)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/bb387098.aspx">LINQ to XML</a> (covers “LINQ to XML” section)</div>
</li>
<li>
<div align="justify"><a href="http://www.codeproject.com/Articles/87621/Introduction-to-XML-and-XSLT-in-C-Net">Introduction to XML and XSLT in C#.Net – CodeProject</a> (covers “transform XML by using XSLT transformations” section)</div>
</li>
<li>
<div align="justify">XMLReader (<a href="http://msdn.microsoft.com/en-us/library/system.xml.xmlreader.aspx">http://msdn.microsoft.com/en-us/library/system.xml.xmlreader.aspx</a>)</div>
</li>
<li>
<div align="justify">XMLWriter (<a href="http://msdn.microsoft.com/en-us/library/system.xml.xmlwriter.aspx">http://msdn.microsoft.com/en-us/library/system.xml.xmlwriter.aspx</a></div>
</li>
<li>
<div align="justify">XMLDocument (<a href="http://msdn.microsoft.com/en-us/library/system.xml.xmldocument">http://msdn.microsoft.com/en-us/library/system.xml.xmldocument</a>)</div>
</li>
<li>
<div align="justify">XSLT (<a href="http://msdn.microsoft.com/en-us/library/126k9kx5.aspx">http://msdn.microsoft.com/en-us/library/126k9kx5.aspx</a> and <a href="http://msdn.microsoft.com/en-us/library/14689742.aspx">http://msdn.microsoft.com/en-us/library/14689742.aspx</a>)</div>
</li>
<li>
<div align="justify"><a href="http://www.codeproject.com/Articles/9494/Manipulate-XML-data-with-XPath-and-XmlDocument-C">http://www.codeproject.com/Articles/9494/Manipulate-XML-data-with-XPath-and-XmlDocument-C</a></div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/library/bb308960.aspx">.NET Language-Integrated Query for XML Data</a></div>
</li>
</ul>
<h2><b></b></h2>
<h2><b>Querying and Manipulating Data by Using the Entity Framework (20%)</b></h2>
<p>&#160;</p>
<h3 align="justify"><i><font style="font-weight:bold;">Query and manipulate data by using the Entity Framework.</font></i></h3>
<p align="justify">This objective may include but is not limited to: Query, update, and delete data by using DbContext; build a query that uses deferred execution; implement lazy loading and eager loading; create and run compiled queries; query data by using Entity SQL</p>
<ul>
<li>
<div align="justify"><a href="http://blogs.msdn.com/b/charlie/archive/2007/12/09/deferred-execution.aspx">LINQ and Deferred Execution</a> (covers “build a query that uses deferred execution” and “query data by using Entity SQL” sections)</div>
</li>
<li>
<div align="justify"><a href="http://weblogs.asp.net/dotnetstories/archive/2011/03/10/lazy-loading-eager-loading-explicit-loading-in-entity-framework-4.aspx">Lazy Loading,Eager Loading,Explicit Loading in Entity Framework</a> (covers “build a query that uses deferred execution” and “implement lazy loading and eager loading” sections)</div>
</li>
<li>
<div align="justify">Deferred execution (<a href="http://msdn.microsoft.com/en-us/library/bb738633.aspx">http://msdn.microsoft.com/en-us/library/bb738633.aspx</a>)</div>
</li>
<li>
<div align="justify">Lazy loading and eager loading, IQueryable vs. IEnumerable (<a href="http://channel9.msdn.com/blogs/matthijs/linq-tips-tricks-and-optimizations-by-scott-allen">http://channel9.msdn.com/blogs/matthijs/linq-tips-tricks-and-optimizations-by-scott-allen</a>)</div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/data/jj574232.aspx">Loading Related Entities</a></div>
</li>
</ul>
<p align="justify"><i></i></p>
<h3 align="justify"><i><font style="font-weight:bold;">Query and manipulate data by using Data Provider for Entity Framework</font></i></h3>
<p align="justify">This objective may include but is not limited to: Query and manipulate data by using Connection, DataReader, Command from the System.Data.EntityClient namespace; perform synchronous and asynchronous operations; manage transactions (API)</p>
<ul>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/bb358362.aspx">System.Data.EntityClient Namespace</a> (covers “Query and manipulate data by using Connection, DataReader, Command from the System.Data.EntityClient namespace” section)</div>
</li>
<li>
<div align="justify"><a href="http://odetocode.com/Blogs/scott/archive/2012/08/26/async-in-entity-framework-6-0.aspx">Async in Entity Framework 6.0</a> (covers “perform synchronous and asynchronous operations” section)</div>
</li>
<li>
<div align="justify"><a href="http://www.mindfiresolutions.com/How-to-use-Transaction-in-Entity-FrameWork-1240.php">How to use Transaction in Entity FrameWork?</a>, <a href="http://social.technet.microsoft.com/wiki/contents/articles/3740.entity-framework-faq-connections-and-transactions.aspx">Entity Framework FAQ: Connections and Transactions</a>, and <a href="http://msdn.microsoft.com/en-us/library/bb336792.aspx">SaveChanges Method</a> (covers “manage transactions (API)” section)</div>
</li>
</ul>
<h3 align="justify"><i><font style="font-weight:bold;"></font></i></h3>
<h3 align="justify"><i><font style="font-weight:bold;">Query data by using LINQ to Entities.</font></i></h3>
<p align="justify">This objective may include but is not limited to: query data by using LINQ operators (for example, project, skip, aggregate, filter, and join); log queries; implement query boundaries (IQueryable vs. IEnumerable)</p>
<ul>
<li>
<div align="justify"><a href="http://code.msdn.microsoft.com/101-LINQ-Samples-3fb9811b">101 LINQ Samples in C#</a> (covers “query data by using LINQ operators (for example, project, skip, aggregate, filter, and join)” section)</div>
</li>
<li>
<div align="justify"><a href="http://jonkruger.com/blog/2007/10/19/iqueryable-vs-ienumerable-in-linq-to-sql-queries/">IQUERYABLE&lt;T&gt; VS. IENUMERABLE&lt;T&gt; IN LINQ TO SQL QUERIES</a> (covers “implement query boundaries (IQueryable vs. IEnumerable)” section)</div>
</li>
<li>
<div align="justify">Query using linq to entities (<a href="http://msdn.microsoft.com/en-us/data/jj573936">http://msdn.microsoft.com/en-us/data/jj573936</a> and <a href="http://pluralsight.com/training/Courses/TableOfContents/querying-entity-framework">http://pluralsight.com/training/Courses/TableOfContents/querying-entity-framework</a>)</div>
</li>
</ul>
<h3 align="justify"><i><font style="font-weight:bold;"></font></i></h3>
<h3 align="justify"><i><font style="font-weight:bold;">Query and manipulate data by using ADO.NET</font></i></h3>
<p align="justify">This objective may include but is not limited to: Query and manipulate data by using Connection, DataReader, Command, DataAdapter, DataSet; Perform synchronous and asynchronous operations; Manage transactions (API)</p>
<ul>
<li>
<div align="justify">· <a href="http://msdn.microsoft.com/en-us/library/8t72t3k4.aspx">System.Data.SqlClient Namespace</a> (covers “Query and manipulate data by using Connection, DataReader, Command, DataAdapter, DataSet” section)</div>
</li>
<li>
<div align="justify">· <a href="http://odetocode.com/Blogs/scott/archive/2012/08/26/async-in-entity-framework-6-0.aspx">Async in Entity Framework 6.0</a> (duplicate reference from above) (covers “perform synchronous and asynchronous operations” section)</div>
</li>
<li>
<div align="justify">· <a href="http://www.mindfiresolutions.com/How-to-use-Transaction-in-Entity-FrameWork-1240.php">How to use Transaction in Entity FrameWork?</a>, <a href="http://social.technet.microsoft.com/wiki/contents/articles/3740.entity-framework-faq-connections-and-transactions.aspx">Entity Framework FAQ: Connections and Transactions</a>, and <a href="http://msdn.microsoft.com/en-us/library/bb336792.aspx">SaveChanges Method</a> (duplicate reference from above) (covers “manage transactions (API)” section)</div>
</li>
<li>
<div align="justify">· Query using ado.net, Connection, DataReader, Command, DataAdapter, DataSet (<a href="http://msdn.microsoft.com/en-us/library/8t72t3k4.aspx">http://msdn.microsoft.com/en-us/library/8t72t3k4.aspx</a>)</div>
</li>
</ul>
<h3 align="justify"><i><font style="font-weight:bold;"></font></i></h3>
<h3 align="justify"><i><font style="font-weight:bold;">Create an Entity Framework data model.</font></i></h3>
<p align="justify">This objective may include but is not limited to: Structure the data model using Table per type, table per class, table per hierarchy; Choose and implement an approach to manage a data model (code first vs. model first vs. database first); implement POCO objects; Describe a data model by using conceptual schema definitions, storage schema definition, and mapping language (CSDL, SSDL, MSL)</p>
<ul>
<li>
<div align="justify">General (<a href="http://msdn.microsoft.com/en-us/data/ee712907">http://msdn.microsoft.com/en-us/data/ee712907</a> )</div>
</li>
<li>
<div align="justify">Whats new: <a href="http://msdn.microsoft.com/en-us/library/ex6y04yf.aspx">http://msdn.microsoft.com/en-us/library/ex6y04yf.aspx</a> )</div>
</li>
<li>
<div align="justify"><a href="http://www.devproconnections.com/article/entity-framework/entity-framework-5-143875">EF 5</a></div>
</li>
</ul>
<h2><font style="font-weight:bold;"></font></h2>
<h2><font style="font-weight:bold;">Designing and Implementing WCF Services (19%)</font></h2>
<p>&#160;</p>
<ul>
<li><a href="http://pluralsight.com/training/courses/TableOfContents?courseName=wcf-fundamentals&amp;highlight=aaron-skonnard_introducing-wcf%2a9#introducing-wcf">Introducing-wcf - Pluralsight</a></li>
<li><a href="http://pluralsight.com/training/courses/TableOfContents?courseName=wcf-extensibility">WCF Extensibility</a></li>
</ul>
<h3><i><font style="font-weight:bold;"></font></i></h3>
<h3><i><font style="font-weight:bold;">WCF Links resource</font></i></h3>
<ul>
<li><a href="http://www.israelaece.com/post/Conteudo-de-WCF-para-estudo.aspx">http://www.israelaece.com/post/Conteudo-de-WCF-para-estudo.aspx</a></li>
<li><a href="http://www.israelaece.com/post/WCF-Videos.aspx">http://www.israelaece.com/post/WCF-Videos.aspx</a></li>
<li><a href="http://msdn.microsoft.com/en-us/library/ee958158%28v=MSDN.10%29.aspx">Introducing Windows Communication Foundation in .NET Framework 4</a></li>
<li><a href="http://msdn.microsoft.com/en-us/library/cc512374%28v=MSDN.10%29.aspx">Windows Communication Foundation: Application Deployment Scenarios</a></li>
<li><a href="http://msdn.microsoft.com/en-us/library/ms734712%28v=VS.100%29.aspx">Getting Started Tutorial</a></li>
<li><a href="http://www.jamesjfoster.com/blog/2010/resource-links-for-70-513-wcf-certification-exam">http://www.jamesjfoster.com/blog/2010/resource-links-for-70-513-wcf-certification-exam</a></li>
<li><a href="http://www.pedrofernandes.net/2012/01/13/material-para-o-exame-wcf-70-513">http://www.pedrofernandes.net/2012/01/13/material-para-o-exame-wcf-70-513</a></li>
<li><a href="http://msdn.microsoft.com/library/ms731197%28VS.100%29.aspx">Guidelines and Best Practices</a></li>
<li><a href="http://msdn.microsoft.com/library/dd483346%28VS.100%29.aspx">Windows Communication Foundation (WCF) Samples</a></li>
<li><a href="http://msdn.microsoft.com/en-us/library/ms731055.aspx">Administration and Diagnostics</a></li>
<li><a href="http://www.dasblonde.net/2007/06/24/WCFWebcastSeries.aspx">http://www.dasblonde.net/2007/06/24/WCFWebcastSeries.aspx</a></li>
</ul>
<h3><font style="font-weight:bold;"></font></h3>
<h3><i><font style="font-weight:bold;">Create a WCF service</font></i></h3>
<p>This objective may include but is not limited to: Create contracts (service, data, message, callback, and fault); implement message inspectors; implement asynchronous operations in the service</p>
<ul>
<li>o What´s new: <a href="http://msdn.microsoft.com/en-us/library/dd456789.aspx">http://msdn.microsoft.com/en-us/library/dd456789.aspx</a></li>
<li>o General (<a href="http://msdn.microsoft.com/en-us/library/bb412204.aspx">http://msdn.microsoft.com/en-us/library/bb412204.aspx</a> , <a href="http://pluralsight.com/training/courses/TableOfContents?courseName=wcf-extensibility">http://pluralsight.com/training/courses/TableOfContents?courseName=wcf-extensibility</a>&#160; )</li>
<li>o Create a service (<a href="http://msdn.microsoft.com/en-us/library/bb412178.aspx">http://msdn.microsoft.com/en-us/library/bb412178.aspx</a> and <a href="http://msdn.microsoft.com/en-us/library/bb924552.aspx">http://msdn.microsoft.com/en-us/library/bb924552.aspx</a>&#160; and <a href="http://msdn.microsoft.com/en-us/library/cc681221.aspx">http://msdn.microsoft.com/en-us/library/cc681221.aspx</a> and <a href="http://msdn.microsoft.com/en-us/library/cc656724.aspx">http://msdn.microsoft.com/en-us/library/cc656724.aspx</a> )</li>
<li>o Understand contracts (<a href="http://msdn.microsoft.com/en-us/library/bb412196.aspx">http://msdn.microsoft.com/en-us/library/bb412196.aspx</a>)</li>
<li>o Synchronous and asynchronous operations (<a href="http://msdn.microsoft.com/en-us/library/ms731177.aspx">http://msdn.microsoft.com/en-us/library/ms731177.aspx</a> , <a href="http://blog.vuscode.com/malovicn/archive/2012/01/21/what-is-new-in-wcf-in-net-4-5-taskt-and-async.aspx">http://blog.vuscode.com/malovicn/archive/2012/01/21/what-is-new-in-wcf-in-net-4-5-taskt-and-async.aspx</a>)</li>
<li>o <a href="http://www.israelaece.com/post/WCF-Introducao.aspx">WCF-Introducao(Portuguese)</a></li>
<li>o <b>Servicecontract and mainly properties</b></li>
</ul>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/clip_image006.png"><img title="clip_image006" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="clip_image006" src="http://blob.vitormeriat.com.br/images/clip_image006.png" width="560" height="441" /></a></p>
<p>· <b>Operation Contract and mainly properties</b></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/clip_image007.png"><img title="clip_image007" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="clip_image007" src="http://blob.vitormeriat.com.br/images/clip_image007.png" width="560" height="414" /></a></p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/clip_image009.png"><img title="clip_image009" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="clip_image009" src="http://blob.vitormeriat.com.br/images/clip_image009.png" width="560" height="373" /></a></p>
<p><b>Examples</b></p>
<p>· Contract </p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/clip_image010.png"><img title="clip_image010" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="clip_image010" src="http://blob.vitormeriat.com.br/images/clip_image010.png" width="560" height="364" /></a></p>
<p>· Service Implementation</p>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/clip_image011.png"><img title="clip_image011" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="clip_image011" src="http://blob.vitormeriat.com.br/images/clip_image011.png" width="560" height="392" /></a></p>
<h3 align="justify"><i><font style="font-weight:bold;">Configure WCF services by using configuration settings</font></i></h3>
<p align="justify">This objective may include but is not limited to: Configure service behaviors; Configure service endpoints; configure binding; specify a service contract; expose service metadata (XSDs, WSDL, and metadata exchange endpoint)</p>
<ul>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/ms733830.aspx">Configuration (endpoints, bindings) by API and config files</a></div>
</li>
<li>
<div align="justify"><a href="http://msdn.microsoft.com/en-us/library/ms751498.aspx">Expose service metadata (XSD, WSDL, exchange) </a></div>
</li>
</ul>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/clip_image012.png"><img title="clip_image012" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="clip_image012" src="http://blob.vitormeriat.com.br/images/clip_image012.png" width="560" height="613" /></a></p>
<h3><i><font style="font-weight:bold;"></font></i></h3>
<h3><i><font style="font-weight:bold;">Configure WCF services by using the API</font></i></h3>
<p align="justify">This objective may include but is not limited to: Configure service behaviors; Configure service endpoints; configure binding; specify a service contract; Expose service metadata (XSDs, WSDL, and metadata exchange); WCF routing and discovery features</p>
<ul>
<li><a href="http://msdn.microsoft.com/en-us/library/ms733830.aspx">Configuration (endpoints, bindings) by API and config files</a></li>
<li><a href="http://msdn.microsoft.com/en-us/library/ms751498.aspx">Expose service metadata (XSD, WSDL, exchange) </a></li>
<li><a href="http://msdn.microsoft.com/en-us/library/ee517421.aspx">Routing </a>and <a href="http://msdn.microsoft.com/en-us/library/dd456782.aspx">discovery</a></li>
<li><a href="http://msdn.microsoft.com/en-us/library/dd456783.aspx">How to: Programmatically Add Discoverability to a WCF Service and Client</a></li>
<li>Address resources; implement filtering; create a query expression; access payload formats (including JSON); use data service interceptors and service operators</li>
<li>Security (<a href="http://pluralsight.com/training/Courses/TableOfContents/iac-wcf">http://pluralsight.com/training/Courses/TableOfContents/iac-wcf</a>)</li>
</ul>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/clip_image014.png"><img title="clip_image014" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="clip_image014" src="http://blob.vitormeriat.com.br/images/clip_image014.png" width="560" height="232" /></a></p>
<p>&#160;</p>
<h3><i><font style="font-weight:bold;">Secure a WCF service</font></i></h3>
<p align="justify">This objective may include but is not limited to: Implement message level security, implement transport level security; implement certificates</p>
<ul>
<li>
<div align="justify"><a href="http://www.israelaece.com/post/WCF-Seguranca.aspx">Segurança Overview (Portuguese)</a></div>
</li>
</ul>
<p align="justify">&#160;</p>
<h3 align="justify"><i><font style="font-weight:bold;">Consume WCF services</font></i></h3>
<p align="justify">This objective may include but is not limited to: Generate proxies by using SvcUtil; generate proxies by creating a service reference; create and implement channel factories</p>
<ul>
<li><a href="http://www.israelaece.com/post/WCF-e28093-Roteamento-de-Mensagens.aspx">Roteamento de Mensagens</a>(portuguese)</li>
</ul>
<p><a href="http://blob.vitormeriat.com.br/images/2013/12/clip_image015.png"><img title="clip_image015" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;"   alt="clip_image015" src="http://blob.vitormeriat.com.br/images/clip_image015.png" width="560" height="103" /></a></p>
<h3><i><font style="font-weight:bold;"></font></i></h3>
<h3><i><font style="font-weight:bold;">Version a WCF service</font></i></h3>
<p align="justify">This objective may include but is not limited to: Version different types of contracts (message, service, data); configure address, binding, and routing service versioning</p>
<p align="justify">Versioning (<a href="http://msdn.microsoft.com/en-us/library/ms731138.aspx">http://msdn.microsoft.com/en-us/library/ms731138.aspx</a>)</p>
<p align="justify">&#160;</p>
<h3 align="justify"><i><font style="font-weight:bold;">Create and configure a WCF service on Windows Azure</font></i></h3>
<p align="justify">This objective may include but is not limited to: Create and configure bindings for WCF services (Azure SDK-- extensions to WCF); Relay bindings to Azure using service bus endpoints; integrate with the Azure service bus relay</p>
<p align="justify">Create on Azure (.net4: <a href="http://www.dotnetcurry.com/ShowArticle.aspx?ID=819">http://www.dotnetcurry.com/ShowArticle.aspx?ID=819</a>) </p>
<h3><i><font style="font-weight:bold;"></font></i></h3>
<h3><i><font style="font-weight:bold;">Implement messaging patterns</font></i></h3>
<p>This objective may include but is not limited to: Implement one way, request/reply, streaming, and duplex communication; implement Windows Azure Service Bus and Windows Azure Queues</p>
<ul>
<li>Messaging patterns (one-way, request/reply, streaming, duplex) (<a href="http://msdn.microsoft.com/en-us/library/ms733070.aspx">http://msdn.microsoft.com/en-us/library/ms733070.aspx</a> )</li>
<li>Azure messaging patterns (azure service bus, azure queues) (<a href="http://pluralsight.com/training/courses/TableOfContents?courseName=azure-sb">http://pluralsight.com/training/courses/TableOfContents?courseName=azure-sb</a> )</li>
<li><a href="http://www.israelaece.com/post/WCF-Tipos-de-Mensagens.aspx">Tipos de Mensagens</a> (Portuguese)</li>
</ul>
<p><i></i></p>
<h3><i><font style="font-weight:bold;">Host and manage services</font></i></h3>
<p align="justify">This objective may include but is not limited to: Manage services concurrency (single, multiple, reentrant); Create service hosts; Choose a hosting mechanism; choose an instancing mode (per call, per session, singleton); activate and manage a service by using AppFabric; implement transactional services; host services in an Windows Azure worker role</p>
<ul>
<li>Hosting (<a href="http://msdn.microsoft.com/en-us/library/ms730158.aspx">http://msdn.microsoft.com/en-us/library/ms730158.aspx</a> )</li>
<li>Manage services concurrency (single, multiple, reentrant) (<a href="http://msdn.microsoft.com/en-us/library/ms752260.aspx">http://msdn.microsoft.com/en-us/library/ms752260.aspx</a> )</li>
<li>Instancing mode (per call, per session, singleton) (<a href="http://msdn.microsoft.com/en-us/library/ms752230.aspx">http://msdn.microsoft.com/en-us/library/ms752230.aspx</a> )</li>
<li>Transaction (<a href="http://msdn.microsoft.com/en-us/library/ms751413.aspx">http://msdn.microsoft.com/en-us/library/ms751413.aspx</a> )</li>
<li>Using AppFabric (appfabric section on <a href="http://pluralsight.com/training/courses/TableOfContents?courseName=beginner-azure">http://pluralsight.com/training/courses/TableOfContents?courseName=beginner-azure</a> )</li>
<li>Host in Azure worker role (.net 4: <a href="http://msdn.microsoft.com/en-us/wazplatformtrainingcourse_windowsazurerolecommunicationvs2010lab.aspx">http://msdn.microsoft.com/en-us/wazplatformtrainingcourse_windowsazurerolecommunicationvs2010lab.aspx</a> )</li>
<li><a href="http://www.israelaece.com/post/WCF-Hosting.aspx">Hosting</a>(Portuguese)</li>
<li><a href="http://www.israelaece.com/post/WCF-Gerenciamento-de-Instancias.aspx">Gerenciamento de Instâncias</a>(Portuguese)</li>
<li><a href="http://www.israelaece.com/post/WCF-Sincronizacao.aspx">Sincronização</a>(Portuguese)</li>
</ul>
<p><b></b></p>
<h1><b>Creating and Consuming Web API-based services (18%)</b></h1>
<p>&#160;</p>
<p><a href="http://pluralsight.com/training/courses/TableOfContents?courseName=aspnetwebapi">Introduction to ASP.NET Web-API</a> (PluralSight Video)</p>
<p><a href="http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api">http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api</a></p>
<h3><i><font style="font-weight:bold;"></font></i></h3>
<h3><i><font style="font-weight:bold;">Design a Web API</font></i></h3>
<p>This objective may include but is not limited to: define HTTP resources with HTTP actions; plan appropriate URI space, and map URI space using routing; choose appropriate HTTP method (get, put, post, delete) to meet requirements; choose appropriate format (Web API formats) for responses to meet requirements; plan when to make HTTP actions asynchronous</p>
<p><a href="http://www.developer.com/net/asp/introduction-to-asp.net-web-api.html">http://www.developer.com/net/asp/introduction-to-asp.net-web-api.html</a></p>
<h3><i><font style="font-weight:bold;">Implement a Web API</font></i></h3>
<p>This objective may include but is not limited to: accept data in JSON format (in JavaScript, in an AJAX callback); use content negotiation to deliver different data formats to clients; define actions and parameters to handle data binding; use HttpMessageHandler to process client requests and server responses; implement dependency injection, along with the dependency resolver, to create more flexible applications; implement action filters and exception filters to manage controller execution; implement asynchronous and synchronous actions; implement streaming actions</p>
<ul>
<li><a href="http://www.strathweb.com/2012/07/everything-you-want-to-know-about-asp-net-web-api-content-negotation/">Content negotiation and response types</a></li>
<li><a href="http://www.asp.net/web-api/overview/working-with-http/http-message-handlers%20and%20http:/byterot.blogspot.se/2012/05/aspnet-web-api-series-messagehandler.html">HttpMessageHandler</a></li>
<li><a href="http://www.asp.net/web-api/overview/extensibility/using-the-web-api-dependency-resolver">Dependency injection with dependency resolver</a></li>
<li><a href="http://www.asp.net/web-api/overview/web-api-routing-and-actions/exception-handling">Action and exception filters</a></li>
</ul>
<h3><i><font style="font-weight:bold;">Secure a Web API</font></i></h3>
<p>o This objective may include but is not limited to: implement HTTPBasic authentication over SSL; implement Windows Auth; enable cross-domain requests; prevent cross-site request forgery (XSRF); implement, and extend, authorization filters to control access to the application</p>
<ul>
<li><a href="http://stevescodingblog.co.uk/basic-authentication-with-asp-net-webapi/">Basic Authentication with Asp.Net WebAPI</a> and <a href="http://blogs.msdn.com/b/carlosfigueira/archive/2012/03/09/implementing-requirehttps-with-asp-net-web-api.aspx">Implementing [RequireHttps] with ASP.NET Web API</a> (covers “implement HTTPBasic authentication over SSL” section)</li>
<li><a href="http://msdn.microsoft.com/en-us/library/dd460317%28v=vs.108%29.aspx">AuthorizeAttribute Class</a> (covers “implement Windows Auth” section)</li>
<li><a href="https://github.com/thinktecture/Thinktecture.Web.Http/blob/master/Thinktecture.Web.Http/Formatters/JsonpFormatter.cs">JsonpFormatter.cs</a> (covers “enable cross-domain requests” section)</li>
<li><a href="http://www.codinghorror.com/blog/2008/09/cross-site-request-forgeries-and-you.html">Coding Horror: Cross-Site Request Forgeries and You</a> (covers “prevent cross-site request forgery (XSRF) ” section)</li>
<li><a href="http://www.c-sharpcorner.com/uploadfile/dhananjaycoder/custom-action-filter-in-Asp-Net-mvc-application/">Custom Action Filter in ASP.Net MVC application</a> (covers “implement, and extend, authorization filters to control access to the application” section)</li>
<li><a href="http://www.asp.net/web-api/overview/security/authentication-and-authorization/preventing-cross-site-request-forgery-%28csrf%29-attacksand%20http:/vimeo.com/43603474">Security (XSRF, filters)</a></li>
</ul>
<h3><i><font style="font-weight:bold;">Host and manage Web API</font></i></h3>
<p>This objective may include but is not limited to: host Web API in an ASP.NET app; self-host a Web API in your own process (a Windows service); host services in a Windows Azure worker role; restricting message size; configure the host server for streaming</p>
<ul>
<li>Host as windows service (<a href="http://www.asp.net/web-api/overview/hosting-aspnet-web-api">http://www.asp.net/web-api/overview/hosting-aspnet-web-api</a> and <a href="http://www.piotrwalat.net/hosting-web-api-in-windows-service/">http://www.piotrwalat.net/hosting-web-api-in-windows-service/</a> )</li>
<li>Host in Azure as worker role</li>
<li><a href="http://stackoverflow.com/questions/9453738/how-do-i-configure-the-buffer-size-and-max-message-size-in-the-asp-net-web-api">Restrict message size</a></li>
</ul>
<h3><i><font style="font-weight:bold;">Consume Web API web services</font></i></h3>
<p>This objective may include but is not limited to: consume Web API services by using HttpClient synchronously and asynchronously; send and receive requests in different formats (JSON/HTML/etc.)</p>
<ul>
<li><a href="http://www.strathweb.com/2013/01/asynchronously-streaming-video-with-asp-net-web-api/">Asynchronity and streaming</a></li>
<li><a href="http://www.developer.com/net/asp/consuming-an-asp.net-web-api-using-httpclient.html">Consuming an ASP.NET Web API Using HttpClient</a></li>
<li><a href="http://blogs.msdn.com/b/webdev/archive/2012/08/26/asp-net-web-api-and-httpclient-samples.aspx">List of ASP.NET Web API and HttpClient Samples</a></li>
</ul>
<p><b></b></p>
<h2><b>Deploying Web Applications and Services (19%)</b></h2>
<h3><i><font style="font-weight:bold;"></font></i></h3>
<h3><i><font style="font-weight:bold;">Design a deployment strategy</font></i></h3>
<p>This objective may include but is not limited to: Create an IIS install package; deploy to web farms; deploy a web application by using XCopy; automate a deployment from TFS or Build Server</p>
<p>Strategies (automated build from TFS, XCopy, IIS install package, VIP swap, sets of configs) (Basics and Source control sections in <a href="http://pluralsight.com/training/Courses/TableOfContents/azure-websites">http://pluralsight.com/training/Courses/TableOfContents/azure-websites</a>)</p>
<h3><i><font style="font-weight:bold;">Choose a deployment strategy for a Windows Azure web application</font></i></h3>
<p>This objective may include but is not limited to: Perform an in-place upgrade and VIP swap; configure an upgrade domain; create and configure input and internal endpoints; specify operating system configuration</p>
<h3><i><font style="font-weight:bold;">Configure a web application for deployment</font></i></h3>
<p>This objective may include but is not limited to: switch from production/release mode to debug mode; use SetParameters to set up an IIS app pool, set permissions and passwords); configure WCF endpoints, bindings, and behaviors; transform web.config by using XSLT (for example, across development, test, and production/release environments); configure Azure configuration settings</p>
<ul>
<li><a href="http://msdn.microsoft.com/en-us/library/dd465318%28v=vs.100%29.aspx">Web.config transformations</a></li>
</ul>
<h3><i><font style="font-weight:bold;">Manage packages by using NuGet</font></i></h3>
<p>This objective may include but is not limited to: Create and configure a NuGet package; install and update an existing NuGet package; connect to a local repository cache for NuGet, set up your own package repository</p>
<ul>
<li>NuGet (<a href="http://gregorsuttie.com/2011/01/03/using-a-nuget-local-repository/">http://gregorsuttie.com/2011/01/03/using-a-nuget-local-repository/</a>)</li>
</ul>
<h3><i><font style="font-weight:bold;">Create, configure, and publish a web package</font></i></h3>
<p>This objective may include but is not limited to: Create an IIS InstallPackage; configure the build process to output a web package; apply pre- and post- condition actions to ensure that transformations are correctly applied; include appropriate assets (web content, certificates)</p>
<ul>
<li><a href="http://www.asp.net/web-forms/tutorials/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment">SetParameters to setup IIS app pool</a></li>
</ul>
<h3><i><font style="font-weight:bold;">Share assemblies between multiple applications and servers</font></i></h3>
<p>This objective may include but is not limited to: Prepare the environment for use of assemblies across multiple servers (interning); sign assemblies by using a strong name; deploy assemblies to the global assembly cache; implement assembly versioning; create an assembly manifest; configure assembly binding redirects (for example, from MVC2 to MVC3)</p>
<ul>
<li><a href="http://msdn.microsoft.com/en-us/library/wd40t7ad.aspx">Strong naming</a></li>
<li>Assembly versioning (<a href="http://msdn.microsoft.com/en-us/library/51ket42z.aspx">http://msdn.microsoft.com/en-us/library/51ket42z.aspx</a> )</li>
<li>Assembly binding redirects (<a href="http://msdn.microsoft.com/en-us/library/433ysdt1.aspx">http://msdn.microsoft.com/en-us/library/433ysdt1.aspx</a> )</li>
<li>Deploy to GAC (<a href="http://msdn.microsoft.com/en-us/library/yf1d93sz.aspx">http://msdn.microsoft.com/en-us/library/yf1d93sz.aspx</a> )</li>
</ul>
<p><b></b></p>
<p><strong>Agradecimentos ao <a href="https://www.facebook.com/virok" target="_blank">Victor Hugo do V C Mello</a></strong></p>
<p><strong></strong></p>
<h2><b>Sites de referência</b></h2>
<ul>
<li><a href="http://www.microsoft.com/learning/en/us/exam.aspx?id=70-487">http://www.microsoft.com/learning/en/us/exam.aspx?id=70-487</a></li>
<li><a href="http://alertcoding.wordpress.com/2013/01/09/microsoft-exam-70-487-study-guide/">http://alertcoding.wordpress.com/2013/01/09/microsoft-exam-70-487-study-guide/</a></li>
<li><a href="http://www.bloggedbychris.com/2013/01/09/microsoft-exam-70-487-study-guide/">http://www.bloggedbychris.com/2013/01/09/microsoft-exam-70-487-study-guide/</a></li>
<li><a href="http://www.bloggedbychris.com/2013/01/24/microsoft-exam-70-487-study-notes/">http://www.bloggedbychris.com/2013/01/24/microsoft-exam-70-487-study-notes/</a></li>
<li><a href="http://www.bloggedbychris.com/2013/01/09/awesome-free-online-learning-microsoft-products/">http://www.bloggedbychris.com/2013/01/09/awesome-free-online-learning-microsoft-products/</a></li>
<li><a href="http://code.msdn.microsoft.com/windowsazure/">code samples available</a></li>
<li><a href="http://www.microsoftvirtualacademy.com/tracks/introduction-to-windows-azure">Microsoft Virtual Academy – Introduction to Windows Azure</a></li>
<li><a href="http://devinthefastlane.wordpress.com/2013/06/15/my-study-guide-for-exam-70-487-developing-windows-azure-and-web-services/">http://devinthefastlane.wordpress.com/2013/06/15/my-study-guide-for-exam-70-487-developing-windows-azure-and-web-services/</a></li>
</ul>
<p>&#160;</p>
<p> <b><b>
<p><font color="#777777">&#160;</font></p>
<p></b></b></p>