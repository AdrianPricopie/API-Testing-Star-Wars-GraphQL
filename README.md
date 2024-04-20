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

# Query 
 
## 1. Query_film_with_positive_id_parameter

![Query](https://github.com/AdrianPricopie/API-Testing-Star-Wars-GraphQL/blob/main/Screenshot%202024-04-20%20at%2011.50.34.png)

### JavaScript Test Scripts

The following JavaScript snippets represent test scripts written in Postman for automated testing of the Star Wars GraphQL API. These tests are designed to ensure the correctness and reliability of the API's responses.

```javascript
pm.test('Query is successful', function () {
    pm.response.to.be.ok;
    pm.response.to.have.statusCode(200);
});

pm.test('Response has expected property', function () {
    pm.expect(pm.response.json().data).to.have.property("film");
});

pm.test('Verify title of film', function () {
    const title = pm.response.json().data.film.title;
    pm.expect(title).to.equals("The Empire Strikes Back");
});

pm.test('Verify id', function () {
    const id = pm.response.json().data.film.id;
    pm.expect(id).to.equals("ZmlsbXM6Mg==");
});

pm.test('Fields are of correct type', function () {
    const film = pm.response.json().data.film;
    pm.expect(film.episodeID).to.be.a('number');
    pm.expect(film.openingCrawl).to.be.a('string');
    pm.expect(film.created).to.be.a('string');
    pm.expect(film.director).to.be.a('string');
    pm.expect(film.producers).to.be.an('array');
});

```
## 2. Query_film_with_inexisting_id_parameter

![Query](https://github.com/AdrianPricopie/API-Testing-Star-Wars-GraphQL/blob/main/Screenshot%202024-04-20%20at%2011.50.39.png)

### JavaScript Test Scripts

The following JavaScript snippets represent test scripts written in Postman for automated testing of the Star Wars GraphQL API. These tests are designed to ensure the correctness and reliability of the API's responses.

```javascript
pm.test('Verify Response', function () {
    pm.response.to.be.ok;
    pm.response.to.have.statusCode(200)
});
pm.test('Verify error message for id ', function () {
    const error = pm.response.errors[0];
    // Verifică mesajul de eroare
    pm.expect(error.message).to.equal("No valid ID extracted from ZmlsbXM6Mg");
})
```
## 3.Query all films

![Query](https://github.com/AdrianPricopie/API-Testing-Star-Wars-GraphQL/blob/main/README.md)

### JavaScript Test Scripts

The following JavaScript snippets represent test scripts written in Postman for automated testing of the Star Wars GraphQL API. These tests are designed to ensure the correctness and reliability of the API's responses.

```javascript
pm.test('Query is successful', function () {
    pm.response.to.be.ok;
    pm.response.to.have.statusCode(200)
});
pm.test('Response has expected property', function () {
    pm.expect(pm.response.json().data).to.have.property("allFilms")
});
pm.test('Response contains correct number of films', function () {
    const responseBody = pm.response.json()
    pm.expect(responseBody.data.allFilms.edges.length).to.equal(6);
});
pm.test('Each film has correct fields', function () {
    const films = pm.response.json().data.allFilms.edges;
    films.forEach(film => {
        pm.expect(film.node).to.have.all.keys('title', 'episodeID', 'openingCrawl', 'director', 'producers', 'releaseDate', 'created', 'edited', 'id');
    });
});
// Verificați dacă datele filmului sunt valide
pm.test('Each film has valid data', function () {
    const films = pm.response.json().data.allFilms.edges;
    films.forEach(film => {
        // Verificați data de lansare
        pm.expect(film.node.releaseDate).to.match(/^\d{4}-\d{2}-\d{2}$/);
        
        // Verificați dacă titlul și descrierea filmului nu sunt goale
        pm.expect(film.node.title).to.not.be.empty;
        pm.expect(film.node.openingCrawl).to.not.be.empty;
    });
});
pm.test('Films are in expected order', function () {
    const films = pm.response.json().data.allFilms.edges;
    const expectedOrder = ["A New Hope", "The Empire Strikes Back", "Return of the Jedi", "The Phantom Menace", "Attack of the Clones", "Revenge of the Sith"];
    films.forEach((film, index) => {
        pm.expect(film.node.title).to.equal(expectedOrder[index]);
    });
});
pm.test('Fields are of correct type', function () {
    const films = pm.response.json().data.allFilms.edges;
    films.forEach(film => {
        pm.expect(film.node.episodeID).to.be.a('number');
        pm.expect(film.node.releaseDate).to.be.a('string');
        pm.expect(film.node.created).to.be.a('string');
        pm.expect(film.node.edited).to.be.a('string');
    })
});

```
