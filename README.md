# Digital Humani API

## Install Node.js

First, install nvm as describe here:

    https://github.com/creationix/nvm

Then, install latest Node.js LTS Dubnium (10.x) - End-of-life April 2020

    > nvm install --lts=dubnium
    > nvm alias default lts/dubnium

FIXME: Lamda are limited to Node.js 8.10, maybe we should use this version instead of latest LTS.
FIXME: Do load test to validate DynamoDB choice

## Install dependency

    > npm install

## Install and config serverless

    > npm install -g serverless
    > serverless config credentials --provider aws --key ??? --secret ???

## Deploy

    > sls deploy           # Deploy backend (Lambda and DynamoDB)
    > sls client deploy    # Deploy frontend (a Web page on S3)

## Try backend

    > export BASE="https://g5lkwar2r1.execute-api.ca-central-1.amazonaws.com/dev"
    > curl -H "Content-Type: application/json" -X POST ${BASE}/enterprise -d '{"name": "My shop", "contact": "John"}'
    > curl -X GET ${BASE}/enterprise/abcd1234

## Try frontend

Go to `http://digitalhumani.com.s3-website.ca-central-1.amazonaws.com/index.html`.

## Fixture

   To init DynamoDB table with some fixture

   > cd fixture
   > ./go.sh

## Offline Testing

    > sls offline start
    > export BASE="http://localhost:3000"
    > curl -H "Content-Type: application/json" -X POST ${BASE}/enterprise -d '{"name": "My shop", "contact": "John"}'
    > curl -X GET ${BASE}/enterprise/abcd1234

## Toolchain planning

Dev tools: Node.js, git, (Suggestion: Visual Studio Code [editor], zsh [shell])

Frontend: HTML Page with JQuery and Bootstrap

Backend: Lamda (processing in JavaScript), DynamoDB (Data persistency), API Gateway (manage by serverless)

Backend management tool: serverless, awscli (sudo snap install AWS CLI --classic)

TODO - Documentation: Swagger, Postman collection

TODO - Testing: JEST, Pupperter

### API Route

TODO: Add JSONP capability (`jsonp` or `callback` param)
TODO: Allow POST to work with contentType: 'application/x-www-form-urlencoded' or 'multipart/form-data'

-----

✓ [GET] /enterprise

✓ [POST] /enterprise {name: '', contact: { name: '', email: '', phone: '' }}
✓ [GET] /enterprise/:id
✓ [GET] /enterprise/:id/treeCount/:monthDate
✓ [DELETE] /enterprise/:id
✓ [PATCH] /enterprise/:id {...}

-----

✓ [GET] /user

✓ [POST] /user {name: '', email: '', phone: '' }
✓ [GET] /user/:id
✓ [DELETE] /user/:id
✓ [PATCH] /user/:id {...}

-----

✓ [GET] /project

✓ [POST] /project {name: '', description: '' }
✓ [GET] /project/:id
✓ [DELETE] /project/:id
✓ [PATCH] /project/:id {...}

-----

✓ [GET] /tree

✓ [POST] /tree {enterpriseId: '', projectId: '', userId: '', treeCount: 1 }
✓ [GET] /tree/:uuid
✓ [DELETE] /tree/:uuid

-----

✓ [GET] /report
✓ [GET] /report/enterprise/:enterpriseId/
✓ [GET] /report/enterprise/:enterpriseId/:monthDate

✗ [POST] /report/generate

-----
