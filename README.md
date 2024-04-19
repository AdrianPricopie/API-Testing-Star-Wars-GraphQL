# Star Wars GraphQL API Testing with Postman

This project utilizes Postman to perform automated tests on the Star Wars GraphQL API. It provides a simple and efficient way to verify certain functionalities and correctness of the Star Wars GraphQL API.

## Description 

The application is intended for automated testing of the Star Wars GraphQL API. It uses Postman collections and workspaces to organize and execute tests for various aspects of the API, such as queries for films, characters, planets, etc.

## Usage

1. **Running Tests**: After importing the collection and workspaces into Postman, you can run individual tests or run the entire collection to test the Star Wars GraphQL API.

2. **Analyzing Results**: After tests have been run, analyze the results to verify that all requests were successfully executed and that API responses meet expectations.

## Resources

- [Postman documentation](https://learning.postman.com/docs/introduction/overview/)
- [App api graphQL documentation](https://studio.apollographql.com/public/star-wars-swapi/variant/current/home)
- [GraphQL documentation](https://graphql.org/learn/)

## Configuration

1. **Install Postman**: Make sure you have [Postman](https://www.postman.com/downloads/) installed on your system.

2. **Import Collections and Workspaces**: Download the Postman collection and workspaces files from this repo and import them into Postman.

    ```bash
    git clone https://github.com/AdrianPricopie/API-Testing-Star-Wars-GraphQL.git
    ```

3. **Install Node.js**: If you haven't already, install [Node.js](https://nodejs.org/) on your system.

4. **Install Newman**: After Node.js is installed, you can install Newman globally using npm. Open your terminal and run the following command:

    ```bash
    npm install -g newman
    ```

    This will install Newman globally on your system, allowing you to run the command `newman` from any directory in your terminal.

5. **Running the Collection**: You can run all the tests with this command:

   ```bash
   newman run "TestsSwapiGrapQL.postman_collection.json"
   ```
