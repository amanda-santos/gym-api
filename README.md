<h1 align="center">
  💸 Transactions API
</h1>

<p align="center">
  <img alt="GitHub top language" src="https://img.shields.io/github/languages/top/amanda-santos/gym-api">

  <img alt="Repository size" src="https://img.shields.io/github/repo-size/amanda-santos/gym-api">

  <a href="https://github.com/amanda-santos/gym-api/commits/master">
    <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/amanda-santos/gym-api">
  </a>

  <a href="https://github.com/amanda-santos/gym-api/issues">
    <img alt="Repository issues" src="https://img.shields.io/github/issues/amanda-santos/gym-api">
  </a>
</p>

<p align="center">
  <a href="#-about-the-project">About the project</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-functional-and-non-functional-requirements">Functional and non-functional requirements</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-routes">Routes</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-technologies">Technologies</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-preview">Preview</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-getting-started">Getting started</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-how-to-contribute">How to contribute</a>&nbsp;&nbsp;&nbsp;
</p>

## 📝 About the project

<p>This is a Node.js HTTP Rest API built with Typescript, Fastify, Prisma, PostgreSQL, JWT and other technologies. It enables gym system management, including user sign up and authentication, permissions, gym creation and search, and check-in creation, history, metrics, and validation.</p>

<p>The application is fully tested with unit and end-to-end tests using Vitest and Supertest, and adheres to the SOLID principles.</p>

<p>Access the API through <a href="https://gym-api-ukop.onrender.com/" target="_blank">this</a> link.</p>

<p>It was developed as a part of Ignite Node.js by <a href="https://www.rocketseat.com.br/" target="_blank">Rocketseat</a> 🚀</p>

## ✔️ Requirements and Business Rules

### Functional requirements

- [x] It should be possible to register;
- [x] It should be possible to authenticate;
- [x] It should be possible to obtain the profile of a logged-in user;
- [x] It should be possible to obtain the number of check-ins performed by the logged-in user;
- [x] It should be possible for the user to obtain their check-in history;
- [x] It should be possible for the user to search for nearby gyms (up to 10km);
- [x] It should be possible for the user to search for gyms by name;
- [x] It should be possible for the user to check-in at a gym;
- [x] It should be possible to validate a user's check-in;
- [x] It should be possible to register a gym.

### Business rules

- [x] Users should not be able to register with a duplicate email;
- [x] Users cannot make 2 check-ins on the same day;
- [x] Users cannot check-in if they are not near (100m) the gym;
- [x] Check-ins can only be validated up to 20 minutes after being created;
- [x] Check-ins can only be validated by administrators;
- [x] Gyms can only be registered by administrators.

### Non-functional requirements

- [x] The user's password needs to be encrypted;
- [x] Application data needs to be persisted in a PostgreSQL database;
- [x] All data lists need to be paginated with 20 items per page;
- [x] Users should be identified by a JSON Web Token (JWT).

## 🚃 Routes

<table>
  <tr>
    <th>HTTP Method</th>
    <th>Route</th>
    <th>Description</th>
    <th>Request body</th>
    <th>Requires authentication token?</th>
    <th>Requires admin permission?</th>
  </tr>

  <tr>
    <td>POST</td>
    <td>/users</td>
    <td>Creates a new user</td>
    <td>
      name
      <br />
      email
      <br />
      password
      <br />
      role (ADMIN or MEMBER)
    </td>
    <td>
      
    </td>
    <td>
      
    </td>
  </tr>

  <tr>
    <td>POST</td>
    <td>/sessions</td>
    <td>Authenticates a user</td>
    <td>
      email
      <br />
      password
    </td>
    <td>
      
    </td>
    <td>
      
    </td>
  </tr>

  <tr>
    <td>GET</td>
    <td>/me</td>
    <td>Returns the current logged in user</td>
    <td>N/A</td>
    <td>
      ✔️
    </td>
    <td>
      
    </td>
  </tr>

  <tr>
    <td>POST</td>
    <td>/gyms</td>
    <td>Creates a new gym</td>
    <td>
      title
      <br />
      description
      <br />
      phone
      <br />
      latitude
      <br />
      longitude
    </td>
    <td>
      ✔️
    </td>
    <td>
      ✔️
    </td>
  </tr>

  <tr>
    <td>GET</td>
    <td>/gyms/search?q=:searchText&page=:pageNumber</td>
    <td>Returns a list of gyms with the given query and page</td>
    <td>N/A</td>
    <td>
      ✔️
    </td>
    <td>
      
    </td>
  </tr>

  <tr>
    <td>GET</td>
    <td>/gyms/nearby?latitude=:number&longitude=:number</td>
    <td>Returns a list of gyms near the given location</td>
    <td>N/A</td>
    <td>
      ✔️
    </td>
    <td>
      
    </td>
  </tr>

  <tr>
    <td>POST</td>
    <td>/gyms/:gymId/check-ins</td>
    <td>Creates a new check-in</td>
    <td>
      latitude
      <br />
      longitude
    </td>
    <td>
      ✔️
    </td>
    <td>
      
    </td>
  </tr>

  <tr>
    <td>PATCH</td>
    <td>/check-ins/checkInId/validate</td>
    <td>Marks the given check-in as validated</td>
    <td>N/A</td>
    <td>
      ✔️
    </td>
    <td>
      ✔️
    </td>
  </tr>

  <tr>
    <td>GET</td>
    <td>/check-ins/history</td>
    <td>Returns a list of the user's check-ins</td>
    <td>N/A</td>
    <td>
      ✔️
    </td>
    <td>
      
    </td>
  </tr>

  <tr>
    <td>GET</td>
    <td>/check-ins/metrics</td>
    <td>Returns the user's check-ins metrics</td>
    <td>N/A</td>
    <td>
      ✔️
    </td>
    <td>
      
    </td>
  </tr>
</table>

## 👩🏻‍💻 Technologies

Technologies used to develop this project:

- Node.js
- Typescript
- Fastify
- Prisma
- PostgreSQL
- JWT (JSON Web Token)
- Zod
- TSup
- Vitest
- Supertest

## 🖥 Preview


## ⌨ Getting started

### Running the server

- Create `.env` file based on `.env.example`
- Run `npm i` to install the dependencies
- Start the Postgresql container with `docker-compose up -d`
- Run `npx prisma migrate dev` to run the migrations
- Run the development server with `npm run start:dev`
- Optionally, import the file `insomnia` on Insomnia to test the routes

### Running unit tests

- Run `npm run test`

### Running E2E tests

- Run `npm run test:e2e`

## 🤔 How to contribute

**Make a fork of this repository**

```bash
# Fork using GitHub official command line
# If you don't have the GitHub CLI, use the web site to do that.

$ gh repo fork amanda-santos/gym-api
```

**Follow the steps below**

```bash
# Clone your fork
$ git clone your-fork-url && cd gym-api

# Create a branch with your feature
$ git checkout -b my-feature

# Make the commit with your changes
$ git commit -m 'feat: My new feature'

# Send the code to your remote branch
$ git push origin my-feature
```

After your pull request is merged, you can delete your branch

---

Made with 🧡 by Amanda Santos
