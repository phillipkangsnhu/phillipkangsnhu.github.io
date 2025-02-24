---
title: "Algorithms and Data Structures"
collection: artifacts
type: "Undergraduate course"
permalink: /artifacts/algorithms_and_data_structures
excerpt: ""
---
| Artifact                         | GitHub Link | Download Link |
|----------------------------------|------------|---------------|
| Initial Artifact (Before Enhancements) | [View on GitHub](https://github.com/phillipkangsnhu/CS-499/tree/5576f6853deb3191535deefb915f2dd415426cde) | [Download ZIP](https://github.com/phillipkangsnhu/CS-499/archive/5576f6853deb3191535deefb915f2dd415426cde.zip) |
| Enhanced Artifact | [View on GitHub](https://github.com/phillipkangsnhu/CS-499) | [Download ZIP](https://github.com/phillipkangsnhu/CS-499/archive/refs/heads/main.zip) |

This artifact is the algorithms and data structures portion of my CS-465 Full Stack Development I final project. I created a token bucket algorithm to rate-limit the amount of API calls made to my application to enhance its security and usability.

I included this artifact in my ePortfolio because, along with the enhancement, it showcases my knowledge of how to implement modern algorithms into a functioning codebase. This demonstrates my understanding of the algorithm at a theoretical level and of its usage at a practical level. By integrating this algorithm into ExpressJS’s middleware, I also show my knowledge of modern JavaScript frameworks and how to augment the framework within its parameters. 

Through the process of enhancing this artifact, I found that there could be further updates by limiting tokens per user such that the entire application isn’t halted by one greedy user. I learned about how the middleware system works in ExpressJS, and how extensible it could be for further API development.


## Course Outcomes Examples
### CS-499-03: Algorithmic Design
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`tokenBucket.js`](https://github.com/phillipkangsnhu/CS-499/blob/main/tokenBucket.js#L1-L25)
``` javascript
class TokenBucket {
constructor(capacity, refillRate) {
    this.capacity = capacity; // Max tokens
    this.tokens = capacity;   // Start with a full bucket
    this.refillRate = refillRate; // Tokens added per second
    this.lastRefillTime = Date.now();
}

refill() {
    const now = Date.now();
    const elapsedTime = (now - this.lastRefillTime) / 1000; // Convert ms to sec
    const newTokens = elapsedTime * this.refillRate;
    this.tokens = Math.min(this.capacity, this.tokens + newTokens);
    this.lastRefillTime = now;
}

consume(tokens = 1) {
    this.refill();
    if (this.tokens >= tokens) {
        this.tokens -= tokens;
        return true;
    }
    return false;
}
}
```
</details>  
This implementation of the Token Bucket Algorithm demonstrates advanced algorithmic problem-solving by efficiently managing API rate limiting. The algorithm runs in O(1) time complexity, making it an optimal solution for high-throughput applications. By integrating it into ExpressJS middleware, I successfully applied theoretical algorithmic concepts to real-world API security, ensuring controlled request flow and preventing server overload.
<div style="margin-top: 10px;"></div>
### CS-499-03: Data Structure Design
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`trip.ts`](https://github.com/phillipkangsnhu/CS-499/blob/main/app_admin/src/app/models/trip.ts#L1-L11)
``` typescript
export interface Trip {
    _id: string,
    code: string,
    name: string,
    length: string,
    start: Date,
    resort: string,
    perPerson: string,
    image: string,
    description: string
}
```
</details>  
This Trip interface represents a well-structured and type-safe data model in TypeScript. By explicitly defining properties, it ensures consistency across the application, reducing runtime errors. Implementing strong data typing in JavaScript frameworks like Angular enhances maintainability and scalability, showcasing my ability to design efficient and structured data representations.
<div style="margin-top: 10px;"></div>
### CS-499-05: Security Implementation
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`user.js`](https://github.com/phillipkangsnhu/CS-499/blob/main/app_server/database/models/user.js#L18-L37)
``` javascript
userSchema.methods.setPassword = function(password){
  this.salt = crypto.randomBytes(16).toString('hex');
  this.hash = crypto.pbkdf2Sync(password, this.salt,
  1000, 64, 'sha512').toString('hex');
  };
userSchema.methods.validPassword = function(password) {
  var hash = crypto.pbkdf2Sync(password,
  this.salt, 1000, 64, 'sha512').toString('hex');
  return this.hash === hash;
};
userSchema.methods.generateJwt = function() {
  const expiry = new Date();
  expiry.setDate(expiry.getDate() + 7);
  return jwt.sign({
  _id: this._id,
  email: this.email,
  name: this.name,
  exp: parseInt(expiry.getTime() / 1000, 10),
  }, process.env.JWT_SECRET); // DO NOT KEEP YOUR SECRET IN THE CODE!
};
```
</details>  
This enhancement improves security by implementing cryptographic password hashing and JSON Web Token (JWT) authentication. Using the `crypto` library ensures secure password storage, mitigating risks of password leaks. JWT authentication adds a secure and scalable method for managing user sessions, demonstrating my ability to integrate secure authentication mechanisms within a modern web application.
<div style="margin-top: 10px;"></div>
### CS-499-05: Authentication System
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`authentication.service.ts`](https://github.com/phillipkangsnhu/CS-499/blob/main/app_admin/src/app/services/authentication.service.ts#L14-L32)
``` typescript
public getToken(): string {
 return this.storage.getItem('travlr-token');
}
public saveToken(token: string): void {
 this.storage.setItem('travlr-token', token);
}
public login(user: User): Promise<any> {
 return this.tripDataService.login(user)
 .then((authResp: AuthResponse) =>
this.saveToken(authResp.token));
}
public register(user: User): Promise<any> {
 return this.tripDataService.register(user)
 .then((authResp: AuthResponse) =>
this.saveToken(authResp.token));
}
public logout(): void {
 this.storage.removeItem('travlr-token');
}
```
</details>
This authentication system follows industry best practices by securely handling user login sessions. The getToken() and saveToken() methods ensure safe storage of authentication tokens while preventing unauthorized access. By implementing token-based authentication, I reinforced the system’s security posture, reducing vulnerabilities and ensuring user data privacy.
