**The goal for this project is to help you get fundamentals of backend engineering.** We will be focusing on the following areas:

- Intro to blockchains
- Tools, languages and packages
- Code structure, patterns and organization
- Testing
- Using external APIs
- Exposing APIs

At the end, we want to expose an api that returns the best time for bridging tokens via Stargate or any reasonable bridge.

This repo has some of the code snippets you need for being able to successfully complete this project. Some of the work will be split in weeks so that you can easily follow allow and do the work needed. Here is the rough outline of how we will progress.

:white_check_mark: :white_check_mark: :white_check_mark: **Week 1**: `[Intro to blockchains]` Blockchain concepts and intro

- https://openavenuesfoundation.sharepoint.com/:p:/g/Ef0CDe6GlwNPm2Bdz0Oa2iEB0i-8kQCQZCES9HX5-exxZw?e=l4GbB2
- https://openavenuesfoundation.sharepoint.com/:w:/r/_layouts/15/Doc.aspx?sourcedoc=%7BE1D768D4-80C8-4C71-ACDF-8D63553D8003%7D&file=Project%20timeline.docx&action=default&mobileredirect=true

<br><br>

:white_check_mark: :white_check_mark: :white_check_mark: **Week 2**: `[Tools, languages and packages]` Protect setup and tools

- Nodejs
- Typescript
- PostgreSQL
- GraphQL
- Docker
- Axios / ethers

For this week, the goal is to setup our project so that we can be ready for active development.

- Install software and get familiar with technical stack
  > VSCode
  >
  > > We recomnend using VSCode for writing the code. Feel free to use other code editing and development tools you like.
  > > You can download and install VSCode from here: https://code.visualstudio.com/download
  > > Iterm
  > > Instead of using the built in terminal, download and install iterm2 terminal for a much better experience.
  > > You can download and install iterm2 from here: https://iterm2.com/downloads.html
  > > NodeJs
  > > For this project, we use NodeJs as our server for running Typescript.
  > > You can download and install NodeJS from here: https://nodejs.org/en/download
  > > Node Provider
  > > To be able to connect to any blockchain, you need to use a node provider. You should create a test account with either Alchemy, Infura or QuickNode
  > > Alchemy : https://www.alchemy.com
  > > Infura : https://www.infura.io
  > > QuickNode: https://www.quicknode.com
  > > Docker
  > > We use docker for containers for running databases
  > > You can download docker here: https://www.docker.com
- Create git repo
  > If you do not have a github account, please create one here: https://github.com
  > After that, create a new git repository for this project
  >
  > > Feel free to name the repository whatever name you prefer. I called mine bridge-evaluation-backend
  > > To learn more about how to create a github repository, follow the steps here: https://docs.github.com/en/get-started/quickstart/create-a-repo
- Start a nodejs project with TS
  > Using the github repository before, start a Typescript project using the followig steps
  >
  > > Clone the repostory you created to your local environment. Example is here: https://github.com/git-guides/git-clone

```
git clone <path to remote>
```

> cd into the project folder

```
cd <repository-name>
```

> > Create a new branch called `starting-a-project` to start creating the new project

```
git checkout -b starting-a-project
```

> create the project

```
npm init -y
```

> install typescript

```
npm install typescript --save-dev
```

> Install NodeJS types

```
npm install @types/node --save-dev
```

> create a config file `tsconfig.json`

```
npx tsc --init --rootDir src --outDir build \
--esModuleInterop --resolveJsonModule --lib es6 \
--module commonjs --allowJs true --noImplicitAny true
```

> create a src folder and add an `index.ts` file

```
mkdir src && touch src/index.ts
```

> Open the `index.ts` file and add the following print statement

```
console.log('Hello world!')
```

> verify that everything runs as expected using the following

```
ts-node ./src/index.ts
```

> > you should see a `'Hello world!'` output on the terminal

Congratulations, you have a working project. Let's save this project to git before we proceed.

- Make your first pull request (PR)
  > Now, we want to our code to git
  >
  > > you may need to sign in to git. You can follow the steps here if you run into issues https://docs.github.com/en/get-started/quickstart/set-up-git
  > > if/after we are signed in, let's commit and push our code

```
git commit -am "initializing the project" && git push -u origin starting-a-project
```

> after the branch has been pushed the main, lets create a new PR
>
> > follow the steps here: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request
> > after creating a the PR, merge it to main
> > You can follow the steps here: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/merging-a-pull-request

- Add PostgreSql container to the project
  > first, let's create a new branch called `adding-pg-containers`

```
git checkout main && git pull && git checkout -b adding-postgresql
```

> > before proceeding, make sure you can see your changes from the setup steps above
> > Start your docker
> > go to applications and start the docker application
> > copy the compose file I added to this repository to your project.
> > start the docker containers

```
docker-compose up -d
```

> connect to your postgresql databse using pgadmin

1. Navigate to localhost:5001 and sign in using credentials in the `compose.yml` file (that is, email: admin@admin.com and password: root)
2. Register a server named evaluating-bridges in pgadmin with the following creds
   1. Host-name/Address: `<Container Name of the service named db in compose.yml>`
   2. Port: `<Container Port of the service named db in compose.yml>`
   3. Username: `<POSTGRES_USER env var of the service named db in compose.yml>`
   4. Password: `<POSTGRES_PASSWORD env var of the service named db  compose.yml>`
3. Create a database named `evaluating_bridges_test`
   > Once the following runs, create a PR with the changes and merge it like we did before.

```
git commit -am "initializing the project" && git push -u origin adding-pg-containers
```

> https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request > https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/merging-a-pull-request

- Add postgreSql and typeorm to the project
  > first, let's create a new branch called `adding-pg-and-typeorm`

```
git checkout main && git pull && git checkout -b adding-pg-and-typeorm
```

> > before proceeding, make sure you can see your changes from the setup steps above
> > install postgresql to the project: this it the databases we are going to be using

```
npm install pg
```

> install typeorm

```
npm install typeorm
```

> install reflect-metadata: we need it for typeorm

```
reflect-metadata
```

> copy the `data_source.ts` file I added to this repository to your project.
> copy the `src/index.ts` file I added to this repository to your project.
> run the following to make sure that your database is working
>
> > make sure you have your docker running and your database is up as well.

```
ts-node ./src/index.ts
```

> > you should get the following output: `"[Success] DB is connected"`
> > Once you have everything running, create a PR with the changes and merge it like we did before.

```
git commit -am "initializing the project" && git push -u origin adding-pg-and-typeorm
```

> https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request > https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/merging-a-pull-request

`Bonus`:

- Adding nodedemon to the project
  > Nodedemon enable auto reload of the server whenever the code changes. This means we do not need to manually restart the server every time we change something, thereby saving us time.
  > first, let's create a new branch called `adding-nodedemon`

```
git checkout main && git pull && git checkout -b adding-nodedemon
```

> After that, copy the provided nodemon.json file

> After that, update the package.json to including a `start:dev` script that starts nodedemon

> After that, test that nodedemon is set properly by running the following command:

```
npm run start:dev
```

> After verifying that the server is running with nodedemon, we can push our code .

```
git commit -am "adding-nodedemon" && git push -u origin adding-nodedemon
```

<br><br>

:white_check_mark: :white_check_mark: :white_check_mark: **Week 3**: `[Using external APIs]` `[Intro to blockchains]` Cost of bridging USDC from Ethereum using Stargate

##### Learning Goals

- Intro to smart contracts
- Intro to smart contract tokens: ERC20
- ABIs
- Gas fees
- Writing from blockchains
- Listening to blockchain events - Reading from blockchains - Writing a listener - Parsing the events

##### Assignment: Read and print the cost of bridging USDC from Ethereum using Stargate

`Resource`:

- Ethereum Logs Hands-On with Ethers.js: https://medium.com/@kaishinaw/ethereum-logs-hands-on-with-ethers-js-a28dde44cbb6
- Stargate: https://stargateprotocol.gitbook.io/
- ERC20: https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol

Architecturally, you can either:

- Periodically make a call to get the cost and save to DB: https://stargateprotocol.gitbook.io/stargate/developers/cross-chain-swap-fee
- Or, listen to events, filter those with USDC from Stargate, save the events to the DB

The second option seems better and more straightforward. That is the option we will be using for this project.

`Here is the step by step guide`:

1. Get the address of Stargate router contract: https://etherscan.io/txs?a=0xdf0770df86a8034b3efef0a1bb3c889b8332ff56
2. Get the address of USDC on Ethereum https://etherscan.io/token/0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48
3. Get the ERC20 ABI and save it: https://gist.github.com/veox/8800debbf56e24718f9f483e1e40c35c
4. Create a signature topic for ERC20 Transfer event: signature = ethers.keccak256(ethers.toUtf8Bytes('Transfer(address,address,uint256)'))
5. Create and instance of src/blockchain_reader.ts that listens to new blocks using the listenToBlockHeaders function. Note, you will need to supply the provider url from the previous week. Infura or Alchemy are really good ones
6. Whenever there is a new block, make a call to get events using the `getEvents` function in `src/blockchain_reader.ts` with the following:
   - topics: [signature, ethers.AbiCoder.defaultAbiCoder().encode(["address"], ["0xdf0770df86a8034b3efef0a1bb3c889b8332ff56"])]
   - address: this is the USDC address, that is => 0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48
   - fromBlock: whatever block you want....get use a reasonable starting block from https://etherscan.io/. Ideally, you want a block that is at least 2 days in the past
7. After you get the events
   - Create an instance of the ABI object: abi = new ethers.Interface(ERC20ABI.abi)
   - Parse the logs you are getting back: for each event log do the following, abi.parseLog({ topics: log.topics as string[], data: log.data })
   - For each parsed log print the results and make sure it matches what you are looking for

`Bonus`:

7. For each parsed log, get a transaction receipt using the `getTransactionReceipt` function in `src/blockchain_reader.ts` 8. Print the gasPrice, gasUsed and timestamp from the transaction receipt.

<br><br>

:white_check_mark: :white_check_mark: :white_check_mark: **Week 4**: `[Tools, languages and packages]` Saving data to postgreSQL

##### Learning Goals

- Relational databases and PostgreSQL: learn about relational databases with a focus on PostgreSQL
- Typeorm: learn about ORMs and how to properly use them for interacting with DBs
- Migrations: learn about proper version management for DBs using migrations

##### Assignment: Create a schema to save the transaction data from week 3 in a postgreSQL database

`Resource`:

- Intro to PostgreSQL [https://medium.com/codex/intro-to-postgresql-c8da31335c34]
  - for this step, you can skip the creation of db and use the one we have in the docker container.
  - to start the docker container use the following
    1. docker-compose up -d
    2. open the following url http://localhost:5001/
    3. login using email: admin@admin.com and password: root
- PostgreSQL Tutorial [https://www.postgresqltutorial.com/]
  - only do the following:
    1. Section 1. Querying Data
    2. Section 2. Filtering Data
    3. Section 9. Modifying Data
    4. Section 10. Transactions
    5. Section 12. Managing Tables
    6. Section 13. Understanding PostgreSQL Constraints
    7. Section 14. PostgreSQL Data Types in Depth
- Typeorm [https://typeorm.io/]
  - only dp the following:
    1. installation: [https://typeorm.io/#installation]; we already did this but just do it for completeness
    2. Quick Start: [https://typeorm.io/#quick-start] ; again, we already did this but just finish it for completeness
    3. Step by step guide: [https://typeorm.io/#step-by-step-guide]
    4. Create a model: [https://typeorm.io/#create-a-model]
    5. Create an entity: [https://typeorm.io/#create-an-entity]
    6. Adding table columns: [https://typeorm.io/#adding-table-columns]
    7. Creating a primary column: [https://typeorm.io/#creating-a-primary-column]
    8. Column data types: [https://typeorm.io/#column-data-types]
    9. Creating a new DataSource : [https://typeorm.io/#creating-a-new-datasource]; we already did this but we need it for completeness
    10. Creating and inserting a photo into the database: [https://typeorm.io/#creating-and-inserting-a-photo-into-the-database]
    11. Using Entity Manager: [https://typeorm.io/#using-entity-manager]
    12. Using Repositories: [https://typeorm.io/#using-repositories]
    13. Using QueryBuilder: [https://typeorm.io/#using-querybuilder]

`Here is the step by step guide`:

0. Add all the missing packages using the following: npm i uuid && npm i --save-dev @types/uuid
1. add create-db-migrations, run-db-migrations and revert-db-migrations command scripts to package.json
2. start the the DB docker-compose up -d
3. Decide the data you want to keep in the database
4. Create the transaction table with the columns for the data you want to store
5. Create the database migrations using `npm run create-db-migrations src/migrations/CreateTransactionTable`

- this should create a new file in the `src/migrations/` folder

6. Run the database migrations using `npm run-db-migrations`

- this should actually create a table for you in the the db
- you can verify that the table was created by checking your db using pgadmin

7. Practice reverting db migrations using `revert-db-migrations`

- this will delete your table and all the data in it

<br><br>

:point_right: :point_right: :point_right: **Week 5**: `[Saving data]` Saving data to postgreSQL

##### Learning Goals

- QueryBuilder and PostgreSQL transactions: use atomic operations to save data.

##### Assignment: Store data from week 3 in the postgreSQL and test its integrity

`Resource`:

- Typeorm [https://typeorm.io/]

`Here is the step by step guide`:

1. Create a function in `src/data/transaction.ts` that saves data to the db
2. Call the function from `integrations/event_listener.ts` with the transactions that need to be saved
3. Create a new data file `data/blockchain_indexing_status.ts` for storing the last indexed block
4. Whenever we have successfully indexed a block, update an entry in `data/blockchain_indexing_status.ts` and sync that with `integrations/transfer_events_processor.ts`

<br><br>

:point_right: :point_right: :point_right: **Week 6**: `[Testing]` Testing

##### Learning Goals

- Unit tests: writing unit tests
- Integration tests: writing integration

##### Assignment: Store data from week 3 in the postgreSQL and test its integrity

`Resource`:

- Typeorm [https://typeorm.io/]
- Jest [https://jestjs.io/docs/getting-started]

`Here is the step by step guide`:

1. Add the jest testing framework to your code `yarn add -D jest ts-jest @types/jest`
2. Create a `jest.config.js` file
3. Create for the `create` function in `data/transactions.ts`; add the tests in a file `src/tests/data/transactions.test.ts`
4. Make sure the tests using `yarn test src/tests/data/transactions.test.ts`
5. Create for the `saveTransactions` and `getTransactionTimestampAndInitiator` functions in `services/transaction_service.ts`; add the test in a file `src/tests/services/transaction_service.test.ts`
6. Make sure the tests using `yarn test src/tests/services/transaction_service.test.ts`

**Week 7**: `[Exposing APIs]` GraphQL

- Exposing data to the external world
- Serving requests

**Week 8**: `[Exposing APIs]` Coingecko API + Twitter (optional)

**Week 8**: Wrap up
