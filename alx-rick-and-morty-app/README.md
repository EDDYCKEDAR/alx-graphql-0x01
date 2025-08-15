Task 3: Application of GraphQL in React
Objective

In this task, you will set up a new Rick and Morty application using Next.js, TypeScript, ESLint, and Tailwind CSS. You will integrate Apollo Client to interact with the Rick and Morty GraphQL API, specifically to fetch episode data.

By the end of this task, you will have:

Created a Next.js project with TypeScript, ESLint, and Tailwind CSS.

Installed and set up Apollo Client for GraphQL queries.

Created an Apollo Client setup to connect with the Rick and Morty GraphQL API.

Written a query to retrieve a list of episodes from the API.

Steps to Complete the Task
1. Create a New Project

In the alx-graphql-0x01 directory, create a new Next.js project named alx-rick-and-morty-app:

npx create-next-app@latest alx-rick-and-morty-app --typescript


After the project is created, change the directory to the project folder:

cd alx-rick-and-morty-app

2. Install Dependencies

Install the necessary dependencies for Apollo Client and GraphQL:

npm install @apollo/client graphql
npm install @types/graphql

3. Set Up Apollo Client

Create a directory called graphql in the root of your project:

mkdir graphql


Inside the graphql directory, create a file named apolloClient.ts:

touch graphql/apolloClient.ts


Replace the content of apolloClient.ts with the following code:

import { ApolloClient, InMemoryCache, HttpLink } from "@apollo/client";

// Set up Apollo Client to connect to the Rick and Morty GraphQL API
const client = new ApolloClient({
  link: new HttpLink({
    uri: "https://rickandmortyapi.com/graphql", // API endpoint
  }),
  cache: new InMemoryCache(), // Using InMemoryCache to cache the results
});

export default client;

4. Set Up GraphQL Queries

Create another file in the graphql directory called queries.ts:

touch graphql/queries.ts


Replace the content of queries.ts with the following code to fetch episodes:

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

5. Configure Apollo Provider

Open the _app.tsx file located in the pages directory:

touch pages/_app.tsx


Replace the content of _app.tsx with the following code to integrate Apollo Client with Next.js:

import "@/styles/globals.css";
import type { AppProps } from "next/app";
import { ApolloProvider } from "@apollo/client";
import client from "@/graphql/apolloClient"; // Import the Apollo Client

export default function App({ Component, pageProps }: AppProps) {
  return (
    // Wrap the app with ApolloProvider to provide Apollo Client to the entire app
    <ApolloProvider client={client}>
      <Component {...pageProps} />
    </ApolloProvider>
  );
}

6. Run the Project

Save all the changes and run the project:

npm run dev


Open your browser and navigate to http://localhost:3000 to see the changes.

7. Verify the Integration

Once you have the project up and running, you should have successfully set up Apollo Client and GraphQL in a Next.js project. You can now begin to query the Rick and Morty API to retrieve episode data or extend your app with more GraphQL queries.

File Structure

Your project structure should now look like this:

alx-rick-and-morty-app/
├── graphql/
│   ├── apolloClient.ts
│   └── queries.ts
├── pages/
│   └── _app.tsx
├── styles/
│   └── globals.css
└── tsconfig.json

Conclusion

In this task, you have set up a Next.js project with TypeScript, ESLint, and Tailwind CSS. You have also integrated Apollo Client to make GraphQL queries to the Rick and Morty API, specifically to fetch data related to episodes.
