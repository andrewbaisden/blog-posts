## Introduction

There are so many online platforms for deploying your applications online. If you are a programmer then this is a technical area in that you must have experience. Having your application running locally on [http://localhost:3000](http://localhost:3000) is fine for development purposes when you are still testing your application. This changes however when the time comes for your application to be ready for production. It will need to be hosted on an online platform so that clients and the world can access it.

[Heroku](https://www.heroku.com/home) used to be an amazing FREE platform for deploying your applications online. It supports many of the most popular programming languages like:

- JavaScript
- Ruby
- Java
- PHP
- Python
- Go
- Scala
- Clojure

For beginner programmers and those who are just transitioning into tech the Heroku platform was a very good place to host your applications. Unfortunately, Heroku has now become pay-to-win. The services are now behind a paywall so it's not free to use anymore which takes away its value for being one of the top tier free platforms to use.

> Starting November 28th, 2022, free Heroku Dynos, free Heroku Postgres, and free Heroku Data for Redis® will no longer be available. If you have apps using any of these resources, you must upgrade to paid plans by this date to ensure your apps continue to run and to retain your data.

In this article, we will learn about 5 free Heroku alternatives and how to deploy the front-end for your JavaScript applications to these platforms. Some of these platforms do support other programming languages and frameworks but for simplicity's sake, we will stick with JavaScript and React applications. It is even possible to deploy back-end applications to some of them too. The list is completely unordered and is not listed by rank.

## 5 FREE Heroku alternatives for deployment

### Prerequisites

For this tutorial we will be using the JavaScript framework React and the package manager npm. However in theory it should be a fairly similar setup if you wanted to use another JavaScript framework like Vue, Angular or Svelte. You might need to install these libraries and frameworks before you can use them.

Three of the most popular React build tools are [Next.js](https://nextjs.org/), [Vite.js](https://vitejs.dev/) and [create-react-app](https://reactjs.org/docs/create-a-new-react-app.html). I will be using Next.js mostly but you can use whichever one you want. We just need a basic boilerplate app so the we can try out all of the online platforms.

Create a folder on your desktop called **deployment** and `cd` into it. Now run the commands below to create a React application using Next.js.

```shell
npx create-next-app@latest
```

Give the application a name of **my-app** and run the commands below to complete the setup and get the app running locally on the development server [http://localhost:3000](http://localhost:3000).

```shell
cd my-app
npm install
npm run dev
```

If you go to [http://localhost:3000](http://localhost:3000) you should see the default Next.js project application home screen running in your browser.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664883570/nextjs-app-home-screen_nnchfo.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664883570/nextjs-app-home-screen_nnchfo.jpg)

Some platforms will require the static version of your application so it is a good idea to create a **build** version as well which just has the static files and not the entire application. This is very easy to do just run the commands below to create a build directory which Next.js calls **.next**. Stop the development server from running and then run the commands below.

```shell
npm run build
npm run start
```

Now you should see the exact same screen however it is now using the build files (HTML, CSS, and JS files) and the production server.

### Deploying your applications online

Before we try to deploy our applications to different platforms lets first put it on GitHub. Many of these platforms will let you import an existing project from GitHub so it is in our best interests to have the codebase on GitHub now.

Go to [GitHub](https://github.com/) and create a new repository for this project and give it the name **deployment-practice**.

Use the command line to navigate inside of your **my-app** folder. You should be inside of the folder that has the **node_modules** folder. Next run the commands below inside of that folder.

```shell
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/andrewbaisden/deployment-practice.git
git push -u origin main
```

Refresh your browser window with the GitHub page and you should see your newly created repository and the Next.js codebase which we created earlier.

#### 1. Netlify deployment

Firstly create an account on [Netlify](https://www.netlify.com/).

Go to you dashboard screen and then click the **add new site** button. Select the option to **Import an existing project** and follow the setup screens.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664883382/netlify-setup-01_gpb2gf.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1664883382/netlify-setup-01_gpb2gf.png)

Deploy your application by clicking on the **deploy** button on the deployment screen. When the deployment is complete you will get a url for your web application. Clicking on the link should bring up your application online.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664883385/netlify-setup-02_mmejcx.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1664883385/netlify-setup-02_mmejcx.png)

#### 2. Vercel deployment

Firstly create an account on [Vercel](https://vercel.com/).

Go to you dashboard screen and then click the **Add New...** button. Select the option for **Project** and follow the setup screens.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664884580/vercel-setup-01_su6mjj.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664884580/vercel-setup-01_su6mjj.jpg)

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664884612/vercel-setup-02_nimx68.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664884612/vercel-setup-02_nimx68.jpg)

When you reach the deployment screen click the **Deploy** button and wait for the setup to complete. You should then see a link your website which has now been deployed on Vercel.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664884649/vercel-setup-03_vwx9me.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1664884649/vercel-setup-03_vwx9me.png)

#### 3. AWS deployment

Firstly create an account on [Amazon AWS](https://aws.amazon.com/).

This time we are going to use [Vite.js](https://vitejs.dev/) for creating a React application. The reason why we won't be using Next.js for this example is because we will be using an Amazon S3 bucket and that requires an `index.html` page to be generated. Running the command `npm run build` will create a build folder called `.next` but it wont have an `index.html` file which is needed here. And the same applies when you use [Static HTML Export](https://nextjs.org/docs/advanced-features/static-html-export).

Fortunately it's pretty fast to create a React project using Vite.js. Use the command line to navigate to the root directory inside of the **deployment** folder we created. Now run the commands below to create a React project using Vite.js.

```shell
npm create vite@latest
```

Give the project a name of **my-app-vite** and choose React as the framework. Select either JavaScript or TypeScript. Now run these commands to complete the setup and start the application.

```shell
cd my-app-vite
npm install
npm run dev
```

Your app should be running locally on [http://127.0.0.1:5173/](http://127.0.0.1:5173/).

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664895793/vitejs-app-home-screen_qb8aii.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664895793/vitejs-app-home-screen_qb8aii.jpg)

Lastly run the command `npm run build` to create a build folder called **dist**. This folder will have an `index.html` file and other static assets which is exactly what we need. You can even run the static website files in the **dist** folder using a server like [serve](https://www.npmjs.com/package/serve) if you have it installed. While inside of the folder **my-app-vite** run the command from the command line.

```shell
serve -s dist
```

Alternatively and as a bonus if you have Python installed you can use that too to run static local files! For example I have Python 3 installed so if I wanted to create a HTTP server to serve some local files I would first `cd` into its root directory and then run a command. So in this case `cd` into the root of the **dist** folder and then run the command below.

```shell
python3 -m http.server 8000
```

If you open up a web browser and go to [http://localhost:8000](http://localhost:8000) the app should be running locally on your machine! I am using a Mac and the command might be slightly different for Windows or Linux but you can google it and figure it out.

Now we can finally concentrate on the AWS part of this tutorial. First there is something important that you need to be aware of. AWS does have FREE tiers however you could have to pay it depends on your usage so be careful. They say:

> With S3, there are no minimum fees. You only pay for what you use. Prices are based on the location of your S3 bucket.

It should be fine for this simple example if your application is more complex and uses a lot of data or requires 3rd party API's that could be different. Read the documentation, terms and pricing and make sure you know what you are doing before you get started because you don't want to accidentally get billed a lot of money.

Navigate to the Amazon S3 page and create a bucket. It is highly likely that the website might have a different design because as you know websites change all the time but you should still be able to find the create a bucket link or button.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664896558/aws-setup-01_axoemo.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664896558/aws-setup-01_axoemo.jpg)

When creating a name for your bucket ensure that it is globally unique. You can't use a name that someone else did otherwise you will get an error because its duplication and not unique.

> Bucket name must be globally unique and must not contain spaces or uppercase letters.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664896953/aws-setup-02_fo3s9d.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664896953/aws-setup-02_fo3s9d.jpg)

Select the settings below.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664897451/aws-setup-03_eorjl6.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664897451/aws-setup-03_eorjl6.jpg)

The rest of the settings should be fine as default so create a bucket.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664897591/aws-setup-04_ghywrb.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664897591/aws-setup-04_ghywrb.jpg)

You should now be on a screen that looks similar to the one below which shows your S3 bucket.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664897890/aws-setup-05_jzaoth.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664897890/aws-setup-05_jzaoth.jpg)

Click on your bucket name and find the tab for properties. Now scroll until you find the **Static website hosting** section. I found it at the bottom of the page.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664898122/aws-setup-06_v9kwey.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664898122/aws-setup-06_v9kwey.jpg)

Click on the **edit** button and then select the configuration below. Make sure that static website hosting is enabled and the index document is set to `index.html`. Now save changes.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664898304/aws-setup-07_ai63hz.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664898304/aws-setup-07_ai63hz.jpg)

We are almost done there is just one step left we need to adjust the permissions so that we can get our application to show up publicly online. Click on the permissions tab and scroll down to the **Bucket policy** section and click the **edit** button.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664898715/aws-setup-08_uu0cwt.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664898715/aws-setup-08_uu0cwt.jpg)

Copy and paste the JSON object code but change the resource key-value pair to be the name of your Amazon S3 bucket.

```json
"Resource": "arn:aws:s3:::${your-Amazon-S3-Bucket-Name}$/*"
```

Copy this code but change the resource key-value pair name.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-app-vite-deployment/*"
    }
  ]
}
```

Click on the save button to save the changes. Let's now navigate to the **Objects** tab.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664899321/aws-setup-09_ytxv29.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664899321/aws-setup-09_ytxv29.jpg)

Go to the **dist** folder inside of your **my-app-vite** project and then drag and drop or upload all of the files to that page. Make sure that it is the contents of the **dist** folder and not the **dist** folder itself because the root file needs to be `index.html` it must not be inside of a folder. Click the button to upload the files and go back to the main screen.

Once again click on the tab for **properties** and scroll until you find **Static website hosting**. There should be a URL for your application if you click on it then your application should be live on Amazon S3!

#### 4. Render deployment

Firstly create an account on [Render](https://render.com/).

After your account has been created you should now be on the dashboard page. Click on the **New** button and choose the selection for a **Web Service**. You will probably need to connect your GitHub account so find the repository we created earlier and connect to it.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664962971/render-setup-01_uecaom.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664962971/render-setup-01_uecaom.jpg)

See an example configuration below for the repository. Give it a name and then you can choose any region you want just make sure that it has these settings.

**Environment**: Node
**Branch**: main or master depending on what you called it
**Build Command**: yarn; yarn build
**Start Command**: yarn start

Select the free plan and then scroll to the bottom and click on the **Create Web Service** button.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664963270/render-setup-02_pyxxx6.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664963270/render-setup-02_pyxxx6.jpg)

Wait for the build to complete and think click on the URL and you should see your application deployed online and working on Render. Please be aware that the free plan does have limits similar to how Heroku was.

> Web Services on the free plan are automatically spun down after 15 minutes of inactivity. When a new request for a free service comes in, Render spins it up again so it can process the request. This can cause a response delay of up to 30 seconds for the first request that comes in after a period of inactivity.

#### 5. Microtica deployment

Firstly create an account on [Microtica](https://microtica.com/).

Then choose to import an existing app.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664984559/microtica-setup-01_soyigf.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664984559/microtica-setup-01_soyigf.jpg)

Select a Github repository.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664984616/microtica-setup-02_mik8ss.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664984616/microtica-setup-02_mik8ss.jpg)

Find the repository you created for this project and fill in the information as shown below. Choosing NextJS as the framework should automatically fill in the build spec details. Give your app a name and then save it.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664984670/microtica-setup-03_zqjm58.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664984670/microtica-setup-03_zqjm58.jpg)

For deployment select **Microtica Kubernetes cluster** because its free.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664986722/microtica-setup-04_hyxrxt.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664986722/microtica-setup-04_hyxrxt.jpg)

Lastly, at the bottom, you will find the button for deployment. Wait for the build to complete and then you should have a link that will take you to your live app deployed on Microtica.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1664986814/microtica-setup-05_mon4yw.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1664986814/microtica-setup-05_mon4yw.jpg)

## Final thoughts

So today we learned how to deploy a React front-end to various online platforms and as you can see it is not that challenging. We went through a few online platforms but there are many more out there that you can use. You just need to read through the documentation on how to use each platform.

Check out this list below to see other cool **FREE** Heroku alternatives for deploying front-end, back-end and full-stack applications.

### List of deployment platforms

1. [Adaptable.io](https://adaptable.io/)
2. [Appliku](https://appliku.com/)
3. [AWS](https://aws.amazon.com/)
4. [Back4app](https://www.back4app.com/)
5. [CapRover](https://caprover.com/)
6. [Cloudflare Pages](https://pages.cloudflare.com/)
7. [Coherence](https://www.withcoherence.com/)
8. [Coolify](https://coolify.io/)
9. [Cyclic](https://www.cyclic.sh/)
10. [Deta](https://www.deta.sh/)
11. [Digital Ocean](https://www.digitalocean.com/)
12. [Dokku](https://dokku.com/)
13. [Firebase](https://firebase.google.com/)
14. [Fleek](https://fleek.co/)
15. [Fly](https://fly.io/)
16. [Gigalixir](https://www.gigalixir.com/)
17. [GitHub Pages](https://pages.github.com/)
18. [Google App Engine](https://cloud.google.com/appengine)
19. [HarperDB](https://harperdb.io/)
20. [Koyeb](https://www.koyeb.com/)
21. [Meteor Cloud](https://www.meteor.com/cloud)
22. [Microtica](https://microtica.com/)
23. [MongoDB](https://www.mongodb.com/)
24. [Napkin](https://www.napkin.io/)
25. [Netlify](https://www.netlify.com/)
26. [Northflank](https://northflank.com/)
27. [Patr](https://patr.cloud/)
28. [Qoddi](https://qoddi.com/)
29. [Qovery](https://www.qovery.com/)
30. [Railway](https://railway.app/)
31. [Render.com](https://render.com/)
32. [Supabase](https://supabase.com/)
33. [Surge](https://surge.sh/)
34. [Vercel](https://vercel.com/)
