## TL;DR

In this tutorial, you'll learn how to create the Telegram desktop app as a web app. We will be using PostgreSQL and Next.js in this guide.

## So... you must have heard of the Telegram messaging app right?

Text messages, images, videos, and other file formats can all be sent via the cross-platform instant messaging app Telegram. With features including end-to-end encryption and self-destructing communications, it is renowned for its attention to privacy and security.

The creator Pavel Durov established it in 2013. Along with offering group conversations for up to 200,000 users, Telegram also offers a significant selection of add-ons and customisations from third parties.

## Why are we using Next.js instead of Create React App?

There is no shortage of React build tools out there we could talk for a long time about the differences, advantages and disadvantages of all of them. Today we are just going to mention the highly popular Next.js JavaScript framework and why it has become the most sought-after build tool for React projects these days.

As of writing Next.js currently has 100k thousand stars on GitHub and managed to surpass Create React App back in 2022. Create React App has about 98.8k thousand stars and both values are definitely going to change the most important factor here is that Next.js which was created by [Vercel](https://vercel.com/) has surpassed the official React build tool which was created by Facebook.

For a number of reasons, Next.js is seen as being more flexible than Create React App (CRA):

- **Configurable configuration** - Compared to CRA, Next.js provides a more adaptable and adjustable setup that gives users greater control over the tools and build process.
- **Dynamic routes** - Automatic code splitting and dynamic routing are made possible by Next.js, making it simpler to manage complicated and large-scale systems.
- **Server-side rendering (SSR)** - Next.js comes with built-in support for server-side rendering, which involves pre-rendering pages on the server before sending them to the client. This reduces load time and boosts the search engine optimisation (SEO) of your application.
- **Creating a static website** - Next.js is a flexible alternative for a variety of projects, from dynamic web apps to static websites, as it can also be used to produce static web pages.

Ultimately it comes down to personal preferences and you can't go wrong with either framework. The goal of any project is to have a minimum viable product and both of these tools are more than good enough at accomplishing that.

## There are so many SQL databases why PostgreSQL?

Because PostgreSQL is an open-source database management system, anybody is allowed to use and change it. Because of this, it is a well-liked option for developers and businesses who wish to avoid the expenses related to proprietary databases.

It is also a well-known fact that PostgreSQL is excellent for complicated and demanding applications due to its advanced capabilities like support for stored procedures, triggers, and complex data types. PostgreSQL can readily grow to handle massive volumes of data and users, which makes it an excellent choice for data-intensive applications.

The great thing about it is that PostgreSQL is well-known for its speed and reliability, making it an excellent choice for applications requiring high dependability and uptime. Another advantage is that PostgreSQL has a big and active developer community that contributes to its development, offers support, and creates 3rd party tools and plugins. PostgreSQL is entirely compliant with the SQL language, making it easy to understand and use for developers and assuring that it will be maintained in the foreseeable future.

PostgreSQL is a flexible and well-liked option for a variety of tasks and uses scenarios because of these qualities. As you can see in the diagram here PostgreSQL is ranked number 2 for all respondents but number one for professionals [StackOverFlow 2022 survey](https://survey.stackoverflow.co/2022/#most-popular-technologies-database).

Nonetheless learning SQL means you can use ANY SQL database so in the grand scheme of things they are all winners 🏆

![https://res.cloudinary.com/d74fh3kw/image/upload/v1675795380/stackoverflow-database-2022_jdvpcj.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1675795380/stackoverflow-database-2022_jdvpcj.jpg)

## How to set up PostgreSQL locally on your machine

### Prerequisites

Our application is going to be full-stack you know what that means right? We will need to have a back-end and a front-end architecture.

Our technology stack is going to be the following:

🗄️ **Back-end**: Node.js + Nest.js
📦 **Database**: PostgreSQL
🧑‍💻 **Front-end**: Next.js

The following software must be installed in order to operate with PostgreSQL databases. A great app for managing PostgreSQL databases is [Postgres.app](https://postgresapp.com/). Additionally, [Pgcli](https://www.pgcli.com/), a command line interface for Postgres, has syntax highlighting and auto-completion is recommended too.

When it comes to utilising a GUI to work with PostgreSQL databases, [Valentina Studio](https://www.valentina-db.com/en/valentina-studio-overview) is my preference. It's a fantastic tool because it can connect to databases like MongoDB and MySQL. Alternatives exist, though, such as [PgAdmin](https://www.pgadmin.org/). Use whatever you're most comfortable with, however.

### Setting up a PostgreSQL database for our Telegram app

#### Step 1: Creating the PostgreSQL database

First, make sure that your development environment has been set up and Postgres.app is running.

Run the command shown below to connect to your local PostgreSQL installation by going to the command line now.

```shell
pgcli
```

Now the command shown below can be used to see all of the PostgreSQL databases you have.

```shell
\l
```

To create a database called Telegram, copy and paste the SQL statement below into your pgcli command line window. You should now be able to see every database, including the one we just established, if you use the command `\l` once more in the same window.

```shell
CREATE DATABASE telegram;
```

Use the command below to connect to the database in the same window as the next step.

```shell
\c telegram
```

Lastly, we need to create a table and populate it with data that will be stored in the Instagram database. The SQL code below should be copied and pasted into your command line window.

```sql
CREATE TABLE telegram_profile (



id UUID DEFAULT gen_random_uuid (),



username VARCHAR(100) NOT NULL,



profile_image VARCHAR(500) NOT NULL,



last_message VARCHAR(1000) NOT NULL,



last_message_date VARCHAR(20) NOT NULL



);



INSERT INTO telegram_profile (username, profile_image, last_message, last_message_date)



VALUES ('Lucy', 'profile1.jpg', 'hello there', '2023-02-02'), ('John', 'profile2.jpg', 'how are you?', '2023-02-02'), ('Gemma', 'profile3.jpg', 'good morning!', '2023-02-03'), ('Sam', 'profile4.jpg', 'have a nice day', '2023-02-03'), ('William', 'profile5.jpg', 'whats up?', '2023-02-05'), ('Magdalena', 'profile6.jpg', 'hows it going?', '2023-02-05'), ('Tina', 'profile7.jpg', 'Guess what?', '2023-02-04'), ('Isabella', 'profile8.jpg', 'I know right so cool!', '2023-02-03'), ('Ethan', 'profile9.jpg', 'take care', '2023-02-02'), ('Ava', 'profile10.jpg', 'Send the picture', '2023-02-08');
```

All of the databases, including the one we just established, should be visible when you launch the Postgres.app application on your computer. And you should be able to view the database you established if you connect to Valentina Studio or your preferred database GUI.

Use these PostgreSQL database connection settings here:

**Host**: localhost
**Database**: telegram
**User**: postgres
**Password**: There is no password leave it blank
**Port**: 5432

#### Step 2: Creating the Nest.js back-end

Finally, we will develop the Nest.js back-end and connect it to our PostgreSQL database. After this phase, we will eventually switch to the React Next.js front-end. Now navigate to your desktop or any directory of your choosing and run the commands below to scaffold your project.

The set up will ask you to choose a package manager I am going to use npm but you can use whichever one you want just don't forget to run the correct commands later on.

```shell
mkdir telegram-app
cd telegram-app
nest new backend
```

Prepare to create some controller and service files by opening the project in your code editor. In order to connect to PostgreSQL databases, we will additionally install TypeORM and PostgreSQL in our project. First, use the command line to `cd` into the **backend** folder, then execute the following instructions.

```shell
cd backend
npm install --save pg @nestjs/typeorm typeorm
nest g controller telegram
nest g service telegram
```

Let's tidy up the files a bit before we generate the additional project files. Get rid of these files by deleting them from your project folder:

- `app.service.ts`
- `app.controller.ts`
- `app.controller.spec.ts`

It is now time to make the remaining project files. Run the instructions listed below once you are in the **backend** root folder.

```shell
mkdir src/telegram
touch src/telegram/{telegram.module.ts,telegram.entity.ts,telegram.service.ts,telegram.controller.ts}
mkdir src/telegram/dto
touch src/telegram/dto/telegram.dto.ts
```

Now that we have all the files needed for this project prepared, it's time to add the code. Add the following code to the existing files or change the current code.

There are 7 files in total:

1. `app.module.ts`
2. `telegram.service.ts`
3. `telegram.module.ts`
4. `telegram.entity.ts`
5. `telegram.controller.ts`
6. `dto/telegram.dto.ts`
7. `main.ts`

Here is the `app.module.ts` file.

```typescript
import { Module } from '@nestjs/common';

import { TypeOrmModule } from '@nestjs/typeorm';

import { TelegramController } from './telegram/telegram.controller';

import { TelegramService } from './telegram/telegram.service';

import { TelegramModule } from './telegram/telegram.module';

import { DataSource } from 'typeorm';

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: 'postgres',

      host: 'localhost',

      port: 5432,

      username: 'postgres',

      password: '',

      database: 'telegram',

      entities: ['dist/**/*.entity{.ts,.js}'],

      synchronize: true,
    }),

    TelegramModule,
  ],

  controllers: [TelegramController],

  providers: [TelegramService],
})
export class AppModule {
  constructor(private dataSource: DataSource) {}
}
```

Next, we have the `telegram.service.ts` file.

```typescript
import { Injectable } from '@nestjs/common';

import { InjectRepository } from '@nestjs/typeorm';

import { Repository } from 'typeorm';

import { Telegram } from './telegram.entity';

@Injectable()
export class TelegramService {
  constructor(
    @InjectRepository(Telegram)
    private telegramRepository: Repository<Telegram>
  ) {}

  async findAll() {
    const data = await this.telegramRepository.query(
      `SELECT * FROM telegram_profile`
    );

    try {
      console.log('Data', data);

      return data;
    } catch (error) {
      console.log(error);
    }
  }
}
```

After that comes the `telegram.module.ts` file.

```typescript
import { Module } from '@nestjs/common';

import { TypeOrmModule } from '@nestjs/typeorm';

import { TelegramController } from './telegram.controller';

import { TelegramService } from './telegram.service';

import { Telegram } from './telegram.entity';

@Module({
  imports: [TypeOrmModule.forFeature([Telegram])],

  controllers: [TelegramController],

  providers: [TelegramService],

  exports: [TypeOrmModule],
})
export class TelegramModule {}
```

And now is the `telegram.entity.ts` file.

```typescript
import { Entity, Column, PrimaryGeneratedColumn, BaseEntity } from 'typeorm';

@Entity()
export class Telegram extends BaseEntity {
  @PrimaryGeneratedColumn('uuid')
  id: string;

  @Column()
  username: string;

  @Column()
  profile_image: string;

  @Column()
  last_message: string;

  @Column()
  last_message_date: string;
}
```

We will do the `telegram.controller.ts` file now.

```typescript
import { Controller, Get } from '@nestjs/common';

import { TelegramService } from './telegram.service';

import { TelegramDto } from './dto/telegram.dto';

@Controller('telegramprofiles')
export class TelegramController {
  constructor(private telegramService: TelegramService) {}

  @Get()
  async findAll(): Promise<TelegramDto[]> {
    return await this.telegramService.findAll();
  }
}
```

Just one more to go after the `dto/telegram.dto.ts` file.

```typescript
export class TelegramDto {
  username: string;

  profile_image: string;

  last_message: string;

  last_message_date: string;
}
```

Lastly the `main.ts` file.

```typescript
import { NestFactory } from '@nestjs/core';

import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.enableCors();

  await app.listen(8080);
}

bootstrap();
```

It's time to get the back end running! Run the command below to start the application in watch mode.

```shell
npm run start:dev
```

Go to [http://localhost:8080/telegramprofiles](http://localhost:8080/telegramprofiles) and all of the data which is inside our PostgreSQL database will be returned as JSON in the browser and the console. Our REST API is set up and working lets now move on to the front end.

## Creating a Telegram web app for the desktop app with Next.js

### Starting with a Next.js boilerplate

Let's start by navigating back into the root folder for **telegram-app** so `cd` into it. Now run the commands to create a boilerplate Next.js project.

```shell
npx create-next-app@latest frontend
```

### Developing the Telegram app UI

Our Next.js front end just needs some HTML and CSS code now. Copy the code and put it into the correct files in our project.

Copy and paste this code into the `src/pages/index.js` file.

```javascript
import { useState, useEffect } from 'react';

import '../styles/Home.module.css';

export default function Home() {
  useEffect(() => {
    fetchAPI();
  }, []);

  const [loading, setLoading] = useState(true);

  const [data, setData] = useState([]);

  const fetchAPI = () => {
    const API = 'http://localhost:8080/telegramprofiles';

    fetch(API)
      .then((response) => {
        return response.json();
      })

      .then((data) => {
        setData(data);

        setLoading(false);

        console.log(data);
      });
  };

  return (
    <>
      <div className="header">
        <p>Telegram</p>
      </div>

      <div className="container">
        {loading ? (
          <div>
            <p>Loading...</p>
          </div>
        ) : (
          <div className="sidebar">
            {data.map((profile) => (
              <div className="profile-container">
                <div className="profile">
                  <div className="profile-image-container">
                    <div className="profile-image"></div>
                  </div>

                  <div className="profile-message">
                    <p>{profile.username}</p>

                    <p>{profile.last_message}</p>
                  </div>

                  <div className="profile-date">
                    <p>{profile.last_message_date}</p>
                  </div>
                </div>
              </div>
            ))}
          </div>
        )}

        <div className="main">
          <p>Select a chat to start messaging</p>
        </div>
      </div>
    </>
  );
}
```

And, put this code into the `styles/global.css` file.

```css
@import url('../styles/Home.module.css');

@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

*,
*::before,
*::after {
  margin: 0;

  padding: 0;

  box-sizing: border-box;
}

:root {
  --main-font-family: 'Roboto', sans-serif;

  --main-font-color: #ffffff;

  --main-font-size: 16px;
}

html {
  font-size: var(--main-font-size);
}

body {
  background: #24303f;

  color: #ffffff;
}
```

Lastly, copy and paste this code into the `styles/Home.module.css` file.

```css
.header {
  text-align: center;

  color: #b1bfcf;

  font-weight: bold;

  margin-top: 0.2rem;
}

.container {
  width: 100%;

  display: flex;

  flex-flow: row nowrap;

  justify-content: flex-start;
}

.sidebar {
  background: #1a222c;
}

.profile {
  display: flex;

  flex-flow: row nowrap;
}

.profile:hover {
  background: #3d6a97;
}

.profile-image-container {
  margin: 0.3rem;
}

.profile-image {
  border-radius: 100%;

  width: 3rem;

  height: 3rem;

  background: #baf6af;
}

.profile-message {
  margin-left: 1rem;

  width: 10rem;

  display: flex;

  flex-flow: column nowrap;

  align-items: flex-start;

  justify-content: center;

  border-bottom: 0.01rem solid #b1bfcf;
}

.profile-message p:nth-child(2) {
  color: #b1bfcf;
}

.profile-date {
  margin: 0.5rem 0.5rem 0 0;

  border-bottom: 0.01rem solid #b1bfcf;
}

.profile-date p {
  color: #b1bfcf;

  font-size: 0.8rem;
}

.main {
  display: flex;

  flex-flow: row nowrap;

  justify-content: center;

  width: 100%;
}

.main p {
  margin-top: 40rem;

  color: #b1bfcf;

  background: #1a222c;

  height: 1.7rem;

  border-radius: 1rem;

  padding: 0.5rem;

  font-size: 0.9rem;
}
```

Make sure that your PostgreSQL database, backend and frontend servers are all running. Go to [http://localhost:3000/](http://localhost:3000/) and you should see a demo Telegram application with some data. It's only a simple example but you can see just how much potential there is for creating more advanced applications using this technology stack. If you want to you can even try to add more functionality like another table for people's comments which you can then render in the chat window.

[Socket.IO](https://socket.io/) would be a fantastic package for adding some real-time chat functionality 😉

## Final thoughts

Ultimately, building a rudimentary Telegram desktop app with PostgreSQL and Next.js is a strong combo that delivers a secure, quick, and user-friendly experience. Developers may quickly design dynamic and scalable apps that are optimised for performance and SEO by exploiting the features of Next.js.

PostgreSQL provides a dependable and adaptable database solution that can manage the demands of a high-traffic app, whereas Telegram delivers a comprehensive range of features and customisation opportunities to create a one-of-a-kind user experience. Overall, this stack is an excellent alternative for developers wishing to create modern, feature-rich desktop apps.

## Thanks for reading!

If you found this article useful, then you're probably the kind of human who would appreciate the value Livecycle can bring to front end teams. I'd be thrilled if you [tried our SDK](https://www.sdk.livecycle.io/?utm_source=devto&utm_medium=post&utm_campaign=instagram) on one of your own projects and gave it a spin with your team. 🙏
