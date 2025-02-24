---
title: "Software Design and Engineering"
collection: artifacts
type: "Undergraduate course"
permalink: /artifacts/software_design_and_engineering
excerpt: ""
---
| Artifact                         | GitHub Link | Download Link |
|----------------------------------|------------|---------------|
| Initial Artifact (Before Enhancements) | [View on GitHub](https://github.com/phillipkangsnhu/CS-499/tree/5576f6853deb3191535deefb915f2dd415426cde) | [Download ZIP](https://github.com/phillipkangsnhu/CS-499/archive/5576f6853deb3191535deefb915f2dd415426cde.zip) |
| Enhanced Artifact | [View on GitHub](https://github.com/phillipkangsnhu/CS-499) | [Download ZIP](https://github.com/phillipkangsnhu/CS-499/archive/refs/heads/main.zip) |


This artifact is the application code of my final project of my CS-465 course, Full Stack Development I. It is two separate services, an AngularJS admin portal and an ExpressJS API + web server bundled together. The enhancement I performed was to containerize the applications and have them run in Docker containers to more easily deploy these services while being platform agnostic.

I included this artifact in my ePortfolio so that I can demonstrate my skills of being able to deploy applications that are cloud-native. With many cloud providers having their own branded services, one of the few constants that remain are containerized applications. This allows me to be more marketable to companies who are looking for engineers who can develop and deploy end-to-end. I improved this artifact by creating Dockerfiles for each of the services, and a docker-compose file to orchestrate the deployment of the services into containers. 

This enhancement reflects on my ability to use well-founded techniques to deliver value, and use best-practices to ensure privacy and enhance application security. By containerizing this application, I show industry-readiness and understanding of commonly used technologies.

In the process of enhancing this artifact, I learned how services networking through the containerization software can set up internal DNS, which makes it much simpler to understand which service is calling another instead of having to remember many different ports on localhost. Setting up the Dockerfiles was challenging due to the volumes overwriting dependencies such as node_modules, but I eventually solved this by consulting documentation and debugging within the containers.


## Course Outcomes Examples
### CS-499-01: Collaborative Development
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`README.md`](https://github.com/phillipkangsnhu/CS-499/blob/main/README.md#project-structure)
``` markdown
├── app_server/         # Web server
│   ├── routes/         # Route definitions
│   ├── controllers/    # Controller definitions
│   ├── views/          # HBS templates
│   └── database/       # DB configuration
├── app_api/            # API server
│   ├── config/         # PassportJS config
│   ├── routes/         # Route definitions
│   └── controllers/    # Controller definitions
├── public/             # Static files
├── migrations/         # Database migration files
├── travlr/             # HTML files
└── app_admin/          # Angular admin interface
```
</details>  
This project structure documentation supports collaboration by providing a clear directory layout that enables other developers to quickly understand and navigate the codebase. Well-organized folder structures and naming conventions promote maintainability, ensuring that multiple contributors can efficiently work on different parts of the application without confusion. By documenting the structure, I demonstrate my ability to build and maintain collaborative environments in software engineering.

<div style="margin-top: 10px;"></div>
### CS-499-02: Professional Communication
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`trip-data.service.ts`](https://github.com/phillipkangsnhu/CS-499/blob/main/app_admin/src/app/services/trip-data.service.ts#L17-L33)
``` typescript
  public getTrip(tripCode: string): Promise<Trip> {
    console.log("Inside TripDataService#getTrip");
    return this.http
      .get(this.tripUrl + tripCode)
      .toPromise()
      .then(response => response.json() as Trip[])
      .catch(this.handleError)
  }

  public getTrips(): Promise<Trip[]> {
    console.log("Inside TripDataService#getTrips");
    return this.http
      .get(`${this.apiBaseUrl}trips`)
      .toPromise()
      .then(response => response.json() as Trip[])
      .catch(this.handleError);
  }
```
</details>  
This API service implementation demonstrates professional software engineering practices by following service-oriented architecture principles. The methods use consistent naming conventions, structured error handling, and clean formatting, ensuring readability and maintainability. Effective API design and documentation allow seamless integration with front-end components, reinforcing my ability to develop professional-quality software that is easy to use and extend.

<div style="margin-top: 10px;"></div>
### CS-499-04: Industry Standards
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`Dockerfile`](https://github.com/phillipkangsnhu/CS-499/blob/main/Dockerfile#L1-L16)
``` Dockerfile
FROM node:23

# Set the working directory inside the container
WORKDIR /app

# Copy the current directory contents into the container
COPY . .

# Install any dependencies if package.json exists
RUN if [ -f package.json ]; then npm install; fi

# Expose port 3000
EXPOSE 3000

# Start the container with npm start
CMD ["npm", "run", "start"]
```
</details>  
This Dockerfile follows modern containerization practices, ensuring that the application can be deployed in a consistent and reproducible manner. Containerizing applications makes them platform-agnostic, improving portability across different environments, from local development to cloud-based deployment. By leveraging industry-standard tools like Docker, I demonstrate my ability to implement best practices in software engineering, making applications scalable and maintainable.

<div style="margin-top: 10px;"></div>
### CS-499-05: Security Mindset
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`app.js`](https://github.com/phillipkangsnhu/CS-499/blob/main/app.js#L38-L43)
``` javascript
app.use('/api', (req,res,next) => {
  res.header("Access-Control-Allow-Origin", '*');
  res.header("Access-Control-Allow-Headers", 'Origin, X-Requested-With, Content-Type, Accept, Authorization');
  res.header("Access-Control-Allow-Methods", 'GET, POST, PUT, DELETE');
  next();
});

```
</details>  
This enhancement applies Cross-Origin Resource Sharing (CORS) policies to control access to the API, preventing unauthorized requests from external sources. Properly configured CORS headers mitigate security vulnerabilities, such as cross-site request forgery (CSRF), while ensuring that only authorized clients interact with the API. By implementing this security measure, I demonstrate an understanding of secure web application design, reducing potential attack vectors and improving overall system security.
