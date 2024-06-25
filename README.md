# wildRydes
AWS hosted app using Amplify, Gateway API, Lambda

The application architecture uses AWS Lambda, DynamoDB, API Gateway, Amazon Cognito, and Amplify Console.

Amplify provides git-based continuous deployment and hosting for full-stack web apps. 

Cognito will handle authorization after users have signed up for an account 





After users have a confirmed account (either using the email verification process or a manual confirmation through the console), they will be able to sign in. When users sign in, they enter their username (or email) and password. A JavaScript function then communicates with Amazon Cognito, authenticates using the Secure Remote Password protocol (SRP), and receives back a set of JSON Web Tokens (JWT). The JWTs contain claims about the identity of the user and will be used in the next module to authenticate against the RESTful API you build with Amazon API Gateway.
