## How To Use Environment Variables In Create React App And Netlify?

Environment Variables are essential for the security of your web application. There is a good chance that you are using GitHub to host your project publically. Within that project, if you are using an external API - you are probably using an API key. Now, if you are directly writing that API key in your code - you are sharing it on GitHub. Everyone can use it. They can access your sensitive information. They can exhaust your API Key's rate limit which can even cost you money. Environment Variables (env var) help prevent that. 

So what exactly is an env var? To put it simply, it's a variable whose value is set outside the program. And it can be used inside a program through reference. 

There are many ways to create an env var. In this article, we will focus on using it in Create React App and Netlify.

## Using Create React App

In create-react-app, we first need to create a `.env` file in the root folder (not src!) with the variable name starting with `REACT_APP_`

It will look something like this:


``` 
REACT_APP_API_KEY=fjfjsd23u4fjld
``` 

**Note:** There are no spaces between the variable, equality sign and the value.

Now, you can directly access the env var in your app using `process.env.REACT_APP_API_KEY`

Here's a demo: https://codesandbox.io/s/env-var-6ytmj

Now, add `.env` to your `.gitignore` file

And we are done (at least the first part). You can push your code to GitHub and your API key will not be exposed.

## Using Netlify

Now, if you are using Netlify to deploy your app - the API key is not available. Your app will not work as you expect. We need to set the same env var in Netlify as well.

When you deploy your website to Netlify, click on `Show Advanced` and add a new variable.


![ENV_VAR.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1618754623736/9TtU6Tdg3.png)

 If you have already deployed your website, go to  `Site settings > Build & deploy > Environment > Environment variables` and click on `Edit Variables` and add your env var.

And we are finally done. Now, our API key is secure. This is the basic setup, for more use-cases, please refer to:  

- https://create-react-app.dev/docs/adding-custom-environment-variables/

- https://docs.netlify.com/configure-builds/environment-variables/

