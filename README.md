# MovieAPI

This is the runthrough of the YT-Tutorial "Fullstack Developement with Java Spring Boot, React and MongoDB" Hosted by freeCodeCamp.org. 

Teachers: \
Backend: Farhan Hasin Chodhury\
Frontend: Gavin Lon @GavinLon


See the original Code on the following repos:\
Backend:    https://github.com/fhsinchy/movieist\
Frontend:   https://github.com/GavinLonDigital/movie-gold-v1



# Before you start
I just run through the first part of the tutorials. The backend is done by me. With the React-part/ Frontend I had trouble to follow along, because it is more a codealong, than a tutorial. 

# Start here

## Prerequisites
- Hava Java JDK LTS installed (by this Date 21.01.2023 I used JDK 17) Link: https://www.oracle.com/java/technologies/downloads/#jdk17-windows
- Have an account at MongoDB Atlas https://cloud.mongodb.com
- Install MongoDB Compass for easyaccess to DB
- I use the VSCode-Editor with the following extensions
Extension Pack for Java (there will be additional extensions installed, which I don't write down here), Maven for Java, Bracket Pair Colorization Tool, Error Lens, MongoDB for VS Code, One Dark Pro, vscode-icons, XML Tools


## Step by Step

### 1. Setup MongoDB Atlas
- Go to https://cloud.mongodb.com and create a new vluster
- use a shared one, with the minimum requirements it fits best for developing purposes. Using more power on the cloud will cost some bucks, so choose wisley.
- 


### 2. Initialize Java Spring
- Go to https://start.spring.io/
- On the left side edit the project like needed
In this project I went for a Maven-Project in Java and used the Spring Boot Version 3.0.1
The project metadata is selfexplaining:
group = com.example
artefact = name of application

I went for packaging-format jar and since I installed JDK 17 Java is 17

- On the right side I choose some dependencies I wanted preselected in the jar-File:
I went for Lombok, Sping Weg, Sping Data MongoDB and Spring Boot DevTools

- Wit Generate the project-zip gets generated and downloaded.
- unzip it in the project folder and open it with VSC

### 3. open the configured JavaSpring Projekt and run it 
   1) Error 8080 is blocked by an running process
      1- run netstat -ano  to get pid number
      2- run taskname /fi “pid eq <pid number>”
      3- run taskkill /f /PID <pid number>
   2) Error Whitlabelpage
      1- no routes are set in the project
      2- wit GetMapping and RestController Annotation Routes can be set to the application
      
### 4. make configuration in /main/resources/application.properties
   1) spring.data.mongodb.database=<database-name>
   2) spring.data.mongodb.uri= <connection String>
      
### 5. Create an .env-File for some security and stop leaking credentials by uploading it to github
   1) Spring don't support reading env-Files
      1- add new dependecy 
      2- look at maven repositories for a fitting one
      3- Add Dependency in pom.xml under dependencies with groupId (com.example), artifactI(name of repo) and version
      4- With the dependency from paul schwarz you can access env-Variables by ${env.<variablename>}
      5-   spring.data.mongodb.database=${env.MONGO_DATABASE}
			spring.data.mongodb.uri= mongodb+srv://${env.MONGO_USER}:${env.MONGO_PASSWORD}@${env.MONGO_CLUSTER}
			
### 6. Implementing the Endpoints
   1) in java/de/mikedilexa/movies create the classes Movie.java and Review.java
   2) For referencing relationships use @DocumentReference
      1- look at mongodb reference relationships and do some research
   3) Create MovieController.java class
   4) Requests against an API are done with REST and the urls
      1- Use @RestController and @RequestMapping(<API-URL>)

### 7. Pulling Data from DB
	1. Needed: a service class and a repository class
		In RestApis are multiple Layers
		   Controller: Get Request and give a Response
		   Service: use repository and talks to DB
		   Repository: Access-Layer to DB and get Data back
   2. In Service Class all the possible Services gets implemented (eg. get all movies, get a movie by id, and so on)
   3. In Repository class just the MongoRepository-Class wie Movie and ObjectId gets extended
   4. get Data by some other filed than ObjectID --> Do not reveal this to public
         By defining the string "Optional<Movie> findMovieByImdb(String imdbId);" in the repository-class MongoDB finds everything to get the requested movie


### 8. Adding a review
   1. taking new mongo template
   2. using update movie with new review
   3. push the new review to the repository

   Create a new Review Controller
   
