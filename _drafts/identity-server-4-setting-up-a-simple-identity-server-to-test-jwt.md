---
layout: post
title: Identity Server 4 - setting up a simple identity server to test JWT
date: 2019-09-17 23:00:00 +0000
description: How to set up a simple identity server to test JWT token issuance
heading: How to set up a simple identity server 4 for JWT
categories: security

---
Making a simple Identity Server 4 to test JWT issuance

If you have ever looked at the Identity Server 4 project on GitHub you will be bewildered by the sheer amount of stuff you can download. There are multiple permutations and branches of the software.

The git source is located here: [https://github.com/IdentityServer/IdentityServer4](https://github.com/IdentityServer/IdentityServer4 "https://github.com/IdentityServer/IdentityServer4")

Here is how we got a very simple Identity Server 4 working to test an application which required JWT tokens.

First we downloaded Quickstart 1_ClientCredentials from the many GitHub example projects. It can currently be found here: [https://github.com/IdentityServer/IdentityServer4/tree/master/samples/Quickstarts/1_ClientCredentials](https://github.com/IdentityServer/IdentityServer4/tree/master/samples/Quickstarts/1_ClientCredentials "https://github.com/IdentityServer/IdentityServer4/tree/master/samples/Quickstarts/1_ClientCredentials")

Open Quickstart.sln in Visual Studio and build it. it should build first time. There is no database with this simple project, so no need to worry about setting up the Identity Server dB.

For our API we only needed to change the Config.cs file as follows.

First change method GetApis:

    public static IEnumerable<ApiResource> GetApis()
    
            {
    
                return new List<ApiResource>
    
                {
    
                    new ApiResource("MyAPI", "My API")
    
                };
    
            }

Where it says MyAPI above change to the name of the API for which you wish to issue JWT tokens.

Second change GetClients:

    public static IEnumerable<Client> GetClients()
    
            {
    
                return new List<Client>
    
                {
    
                    new Client
    
                    {
    
                        ClientId = "client",
    
                        // no interactive user, use the clientid/secret for authentication
    
                        AllowedGrantTypes = GrantTypes.ClientCredentials,
    
                        // secret for authentication
    
                        ClientSecrets =
    
                        {
    
                            new Secret("secret".Sha256())
    
                        },
    
                        // scopes that client has access to
    
                        AllowedScopes = { "MyAPI" }
    
                    }
    
                };
    
            }

Be aware that three fields above are critical to how you call your identity server:

ClientId 'client' - the name of the client which will call identity server

ClientSecrets 'secret' - the secret your API will use which identifies that it is a valid caller of identity server for the issuance of JWT tokens

AllowedScopes - the API resource you set up in the previous method.

These three values have to feature in the calling application.

To test that everything is working we can use the venerable PostMan app as follows:

![](https://res.cloudinary.com/goodlycode/image/upload/v1568902831/postman_1.png)

Set up your API get and click on the Authorization tab as above.

You should see this dialogue:

![](https://res.cloudinary.com/goodlycode/image/upload/v1568902831/postman_2.png)

Click on the orange button 'Get New Access Token'

![](https://res.cloudinary.com/goodlycode/image/upload/v1568902831/postman_3.png)

* Select Grant Type of 'Client Credentials'. 
* Enter the URL of your identity server as 'Access Token URL'. 
* Enter the client id you coded into identity server as 'Client ID'
* Enter the secret you coded into identity server as 'Client Secret' 
* Enter the Allowed Scope you coded into identity server as 'Scope'

Press the orange 'Request Token' button.

Postman should then issue a token!

![](https://res.cloudinary.com/goodlycode/image/upload/v1568902831/postman_4.png)

Scroll to the bottom of the dialogue where the Access Token is displayed.

You will see an orange button 'Use Token'

![](https://res.cloudinary.com/goodlycode/image/upload/v1568902831/postman_5.png)

![](https://res.cloudinary.com/goodlycode/image/upload/v1568902831/postman_6.png)