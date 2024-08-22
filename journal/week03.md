# Week 3 — Decentralized Authentication

#### Amazon Cognito
User pools for integrating an application for a pool of users. Web application and you want to create a login  & signup. 
Configured a user pool on the AWS console under the name cruddur-user-pool

- AWS Amplify is a SDK for severless libraries and a hosting platform. A way to provision serverless applications. We can use Cognito only for Javascript through Amplify.
- Search Cognito Amplify AWS on google " https://docs.amplify.aws/react/build-a-backend/auth/ "

#### Configuring AWS Amplify with Cognito User pool
There are changes in the interface connecting AWS Amplify to APP.js. 
Previous code was used to connect using the following: 
``` 
import { Amplify } from 'aws-amplify';

Amplify.configure({
  "AWS_PROJECT_REGION": process.env.REACT_AWS_PROJECT_REGION,
  "aws_cognito_identity_pool_id": process.env.REACT_APP_AWS_COGNITO_IDENTITY_POOL_ID,
  "aws_cognito_region": process.env.REACT_APP_AWS_COGNITO_REGION,
  "aws_user_pools_id": process.env.REACT_APP_AWS_USER_POOLS_ID,
  "aws_user_pools_web_client_id": process.env.REACT_APP_CLIENT_ID,
  "oauth": {},
  Auth: {
    // We are not using an Identity Pool
    // identityPoolId: process.env.REACT_APP_IDENTITY_POOL_ID, // REQUIRED - Amazon Cognito Identity Pool ID
    region: process.env.REACT_AWS_PROJECT_REGION,           // REQUIRED - Amazon Cognito Region
    userPoolId: process.env.REACT_APP_AWS_USER_POOLS_ID,         // OPTIONAL - Amazon Cognito User Pool ID
    userPoolWebClientId: process.env.REACT_APP_AWS_USER_POOLS_WEB_CLIENT_ID,   // OPTIONAL - Amazon Cognito Web Client ID (26-char alphanumeric string)
  }
});
```
This has been changed due to some variables which have changed: 
```
Amplify.configure({

    Auth: {
      Cognito: {
        // identityPoolId: process.env.REACT_APP_IDENTITY_POOL_ID, // REQUIRED - Amazon Cognito Identity Pool ID
        region: process.env.REACT_APP_AWS_PROJECT_REGION,           // YES REQUIRED - Amazon Cognito Region
        userPoolId: process.env.REACT_APP_AWS_USER_POOLS_ID,         // YES OPTIONAL - Amazon Cognito User Pool ID
        userPoolClientId: process.env.REACT_APP_CLIENT_ID,   // yes OPTIONAL - Amazon Cognito Web Client ID (26-char alphanumeric string)
        loginWith: {
          email: true,
        },
        signUpVerificationMethod: "code",
        userAttributes: {
          email: {
            required: true,
          },
        },
        allowGuestAccess: true,
        passwordFormat: {
          minLength: 8,
          requireLowercase: true,
          requireUppercase: true,
          requireNumbers: true,
          requireSpecialCharacters: true,
        },
      },
    },
})

```
Previously, the frontend UI was not loading. This has now been fixed with the code used above. I believe the errors were because of changes in variables from V5 to V6. Few other changes were also made in the following code: 
#### In profileInfo.js
```
import { signOut } from 'aws-amplify/auth';

export default function ProfileInfo(props) {
  const [popped, setPopped] = React.useState(false);

  const click_pop = (event) => {
    setPopped(!popped)
  }
  
  const handleSignOut = async () => {
    try {
        await signOut({ global: true });
        window.location.href = "/"
    } catch (error) {
        console.log('error signing out: ', error);
    }
  }
```

