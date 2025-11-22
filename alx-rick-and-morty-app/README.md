# Rick and Morty GraphQL Application

This project is part of the **ALX GraphQL curriculum**, where you build a React/Next.js application that consumes the **Rick and Morty GraphQL API** using **Apollo Client**. This README explains the setup steps, project structure, and how to move the project directory using shell commands.

---

## 📌 Project Overview

This application connects to the Rick and Morty GraphQL API and fetches data such as episodes, characters, and locations. It is built using:

* **Next.js (TypeScript)**
* **Tailwind CSS**
* **Apollo Client (GraphQL)**
* **ESLint**

The project name is: **alx-rick-and-morty-app**.

---

## 🛠️ Initial Project Setup

### 1. Create the project directory

Inside the `alx-graphql-0x01` directory:

```sh
yarn create next-app alx-rick-and-morty-app --typescript --eslint --tailwind
```

or

```sh
npx create-next-app@latest alx-rick-and-morty-app --typescript --eslint --tailwind
```

---

### 2. Install GraphQL dependencies

```sh
npm install @apollo/client graphql
npm install @types/graphql
```

---

## 📁 GraphQL Setup

### Create the `graphql/` directory

```sh
mkdir graphql
```

### Create Apollo Client file

`graphql/apolloClient.ts`:

```ts
import { ApolloClient, InMemoryCache, HttpLink } from "@apollo/client";

const client = new ApolloClient({
  link: new HttpLink({
    uri: "https://rickandmortyapi.com/graphql",
  }),
  cache: new InMemoryCache(),
});

export default client;
```

### Create GraphQL Queries file

`graphql/queries.ts`:

```ts
import { gql } from "@apollo/client";

export const GET_EPISODES = gql`
  query getEpisodes($page: Int, $filter: FilterEpisode) {
    episodes(page: $page, filter: $filter) {
      info {
        pages
        next
        prev
        count
      }
      results {
        id
        name
        air_date
        episode
      }
    }
  }
`;
```

---

## 🔌 Adding ApolloProvider to Next.js

Open `pages/_app.tsx` and replace its content:

```ts
import "@/styles/globals.css";
import type { AppProps } from "next/app";
import { ApolloProvider } from "@apollo/client/react";
import client from "@/graphql/apolloClient";

export default function App({ Component, pageProps }: AppProps) {
  return (
    <ApolloProvider client={client}>
      <Component {...pageProps} />
    </ApolloProvider>
  );
}
```

> Note: Some Apollo Client versions require you to import ApolloProvider from `@apollo/client/react` instead of `@apollo/client`.

---

## 🚀 Running the Application

### Development mode

```sh
npm run dev
```

Visit: `http://localhost:3000`

### Production mode

You **must build first**:

```sh
npm run build
npm run start
```

If you see this error:

```
Could not find a production build in the '.next' directory
```

It means you forgot to run `npm run build`.

---

## 📦 Moving Project Directories in Shell

If you need to move your project directory using the terminal:

### ✅ Move the folder into another directory

```sh
mv alx-rick-and-morty-app alx/
```

This results in:

```
alx/alx-rick-and-morty-app
```

### ✅ Move and rename the folder

```sh
mv alx-rick-and-morty-app alx/rick-and-morty-app
```

### ❌ Incorrect command example

```
mv alx-rick-and-morty-app alx/rick-and-and-morty-app
```

This renames the folder incorrectly (`and-and`) instead of moving it properly.

---

## 🧹 Removing Git

If you accidentally or intentionally remove your Git repository:

```sh
rm -rf .git
```

You can reinitialize Git:

```sh
git init
git add .
git commit -m "Initial commit"
```

---

## ✔️ Required Files for Submission

Inside `alx-graphql-0x01/alx-rick-and-morty-app`:

* `README.md`
* `graphql/apolloClient.ts`
* `graphql/queries.ts`
* `pages/_app.tsx`

---

## 🎉 Conclusion

You now have a complete React + GraphQL application using Apollo Client and the Rick and Morty API. The setup is fully aligned with your ALX project requirements. Continue by building UI pages and rendering episode data.

If you want help building the Episodes page or integrating pagination, feel free to ask!
