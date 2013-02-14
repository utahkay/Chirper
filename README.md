Chirper

Chirper is a simple twitter clone webapp with an .NET ASP.NET MVC 4 powered front-end and a Cassandra NoSQL back-end

http://www.sinbadsoft.com/blog/chirper-twitter-clone-webapp-with-net-front-end-and-cassandra-nosql-back-end/

* Dependencies:
- Microsoft .NET 4 Framework
- ASP.NET MVC 4
- Aquiles 1.0 library
- DataStax Community Edition
- NuGet
- Twitter Bootstrap 2.1.1

* Tested With:
- DataStax Community Edition 1.1.6 + OpsCenter Community (http://www.datastax.com/products/community)
- Windows 7
- Visual Studio 2010 SP1

* Enhancements and Improvements:
]- Solution updated to Visual Studio 2010
- web app now runs using ASP.NET MVC 4 using Razor View engine instead of ASP.NET MVC 2 and WebFroms view Engine
- now runs using Aquiles 1.0 library

* Cassandra setup

Install DataStax community edition and OpsCenter Community Edition

** Verify cluster name in DataStax OpsCenter Community (top left corner of "Dashboard" view next to Cassandra version number)

NOTE: To open DataStax OpsCenter Community Edition, open a web browser other than Internet Explorer and navigate to http://localhost:8888 

This is the cluster configuration you should have in web.config:

<aquilesConfiguration>
    <clusters>
      <add friendlyName="Test Cluster"> <!-- Cluster name from DataStax OpsCenter Community should match here -->
        <connection poolType="SIZECONTROLLEDPOOL" factoryType="FRAMED"/>
        <endpointManager type="ROUNDROBIN" defaultTimeout="6000">
          <cassandraEndpoints>
            <add address="localhost" port="9160"/>
          </cassandraEndpoints>
        </endpointManager>
      </add>
    </clusters>
  </aquilesConfiguration>

** Chirper Keyspace setup

Open 'Cassandra CLI Utility' (start menu -> DataStax Community Edition)

Type each of the following lines at the prompt:

create keyspace Chirper;
use Chirper;
create column family Users with comparator = UTF8Type;
create column family Tweets with comparator = UTF8Type;
create column family Following with comparator = UTF8Type;
create column family Followers with comparator = UTF8Type;
create column family TimeLine with comparator = UTF8Type;
create column family UserLine with comparator = UTF8Type;

* Roadmap
- link followers count to followers page on main user page
- link following count to following page on main user page
- clicking Chirper in top nav menu brings you back to the main page
- chirp "it&#39;s me bart" should show as "it's me bart"
- do infinite scrolling on chirps (I think it's trying to retrieve and show all at once, just get a bunch at a time)
- when looking at the user's profile:
-- show pie chart of % of followers who are {Male, Female, Unspecified}
-- show pie chart of % of following who are {Male, Female, Unspecified}
- show post activity by day using GitHub profile grid by day visualization
- bootstrap the user action navigation menu
- mimic twitter's layout for showing Tweets
- stay up to date on Twitter Bootstrap
- if not already, deploy somewhere publicly
- add unit tests
- use an IoC container
- create a fake Chirp Repository to test different scenarios
- show assigned permalink to each Chirp
- allow one user to directly send a private Chirp to another user
- enable ReChirp
- in the code and Cassandra, change Tweet -> Chirp
- show chirps using relative time
	x seconds, 
	x mins, 
	x hours,
	x days,
	x months,
	x years ago)
- lost password (currently you can look this up in Cassandra directly since it's not getting encoded in any way)
-- email me my password if I forgot it
-- allow me to reset my password
- mimic behavior of Python Cassandra clone (named ...) and/or Sinatra clone applications mentioned in Cloning applications book ("Cloning Internet Applications with Ruby")
- clean up behavior of "In Reply To"
- use Autofac to inject Repository into controllers (use something like Autofac for Dependency Injection)
- integrate Twitter bootstrap presentation framework into this application
- keep working to clone Twitter using Cassandra and other NoSQL technologies
- show number of users online (using Redis)
- recommend some people to me (send me emails)
- user profile storage
-- store when the user was created (so you can do memeber since..)
-- store user's age/birthday (prompt them for day, month, year) - month and year are required
-- store user's location (geotag)
- find people
-- near me (geotag), near a location
-- find people meeting certain criteria (sex, age group, location)
- do some analytics (perhaps using Hadoop)
-- find users who share tags in common
-- most referenced tags
-- users posting the most chirps (of all time, today, last hour, etc...)
-- count chirps per user
-- count total chirps
-- count total chirps per time period (last day, last hour,...)
-- count chirps with a given tags
-- who chirps more, men or women - per time period (last day, last hour,...)
- internationalization / localization

DONE
- convert views from Web Forms view engine to Razor view engine (IN PROGRESS)
- clean up page titles on each Razor view
- hook up Twitter Bootstrap to this
- user profile storage
-- store user's gender (male or female, or unspecified)
- update more buttons to use bootstrap look and feel
- show # of followers the user has on their main user page
- show # of people following them on the user has on their main user page
- show # of chirps user has posted on their main user page