User Pool name WildRydes
User Pool ID us-east-1_T90mByXWr

App Client ID 6kqe2i1b93ob9tdr4l879imbkk


tests were not working so after changing a few other settings I moved to node14.x
and returned the:

// var AWS = require('aws-sdk');
// import AWS from 'aws-sdk'
// from 'aws-sdk/lib/aws.js' import AWS;
// import AWS from '/var/runtime/node_modules/aws-sdk/lib/aws.js';
// from aws import AWS;

back to:
const AWS = require('aws-sdk');


zF35&icmkNxN5D6z




