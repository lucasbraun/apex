# Building an end-to-end Bookstore App with External Community Modules

## Introduction
In this lab, you will learn how to build an end-to-end bookstore application within a very short time, mainly relying on external community JavaScript modules, the built-in fetch API as well as a tiny little bit of additional JavaScript glueing.
You will utilize the following two external JavaScrip libraries/modules:

- GraphQL
- Mustache

Estimated Lab Time: 20 minutes

## Task 1: First steps with fetch API

### Setting up Access Control
In order to be able to make callouts to public internet, we need to make sure to add the corresponding access control lists. Execute the following script which will prompt you for the schema name from SQL*Plus as sysdba (or ask your administrator to perform it for you):

```
<copy>
declare
    l_hostname varchar2(64) := '*.googleapis.com';
    l_port number := 443;
    l_principal varchar2(64);

    procedure add_priv(p_priv varchar2, p_host varchar2, p_port number) is
    begin
        dbms_network_acl_admin.append_host_ace (
            host       => p_host, 
            lower_port => p_port,
            upper_port => p_port,
            ace        => 
                xs$ace_type(privilege_list => xs$name_list(p_priv),
                            principal_name => l_principal,
                            principal_type => xs_acl.ptype_db));
    end;

    procedure add_priv_resolve(p_host varchar2) is
    begin
        dbms_network_acl_admin.append_host_ace (
            host       => p_host,
            ace        => 
                xs$ace_type(privilege_list => xs$name_list('resolve'),
                            principal_name => l_principal,
                            principal_type => xs_acl.ptype_db)); 
    end;
begin
    l_principal := '&please_enter_schema_name';
    add_priv('connect',l_hostname,l_port);
    add_priv_resolve(l_hostname);
    add_priv('http',l_hostname,l_port);
    commit;
end;
/
</copy>
```

### Setting up the Wallet
The other thing that you need is a wallet and making sure that we set that wallet each time we use `fetch` functionality.
We therefore create a wrapper function `SET_WALLET` as follows.
First go to SQL Workshop -> SQL Commands and choose "PL/SQL" as your language in the top.

![](images/00-sql-commands.png " ")

Next, if you are operating in an Autonomous Database environment or Live Lab sandbox, the wallet is preconfigured, so all you need to do is execute:

```
<copy>
CREATE OR REPLACE PROCEDURE SET_WALLET AS BEGIN NULL; END;
/
</copy>
```

Conversely, if you are in a different environment, you may have to create your wallet first, for instance by following the steps provided in this
[article](https://github.com/Dani3lSun/oracle-ca-wallet-creator).

Once, your wallet is created and installed on the server, create the function as follows (adapt the directory name to match the location of your certificate):

```
<copy>
CREATE OR REPLACE PROCEDURE SET_WALLET AS BEGIN utl_http.set_wallet('file:/opt/oracle/wallet-creation/CAcertBundle'); END;
/
</copy>
```

### Using the fetch API
Now that we have a function for setting the wallet appropriately, we can use the JavaScript fetch API to retrieve our desired book results and print it to the console.
Switch the language in SQL commands to "JavaScript" and excute the following snippet:

```
<copy>
await import('mle-js-fetch');
const BASE_URL = "https://www.googleapis.com/books/v1/volumes?q=";

async function getBooks(searchTerm) {
  session.execute("begin set_wallet; end;");
  const response = await fetch(`${BASE_URL}${searchTerm}`, { credentials: "include" });
  const result = await response.json();
  return result;
}

const bookResults = await getBooks('Oracle');
// book results contains kind (string), totalItems (number), items (objects with the actual books inside)
console.log(`Total Items: ${bookResults.totalItems}`);
console.log(`First Item: ${JSON.stringify(bookResults.items[0])}`);
</copy>
```

If executed correctly, you should see something like this:

![](images/00-simple-fetch.png " ")

We now know how to use the fetch API in principle. We'll use this knowledge again later, in Task 4, to assemble the app as a whole.

## Task 2: Importing GraphQL Module
Our application will make use of the open-source [GraphQL](https://www.npmjs.com/package/graphql) module.
Using GraphQL comes with a number of advantages which are well explained in
[this blog post](https://medium.com/@jeff_long/when-and-why-to-use-graphql-24f6bce4839d).
In our case, we'll use it to combine data retrieved from the Google Books API with some local data in the database and offer this as one unified service.

In order to install the GraphQL module into Oracle as MLE module, fist go to the object browser:

![](images/01-object-browser.png " ")

Then, click on the "+" button in the left pane and select "MLE Module - JavaScript" or simply select this option from the middle pane:

![](images/02-create-mle-module.png " ")

This opens a dialog in which you provide the name of your module, `GRAPHQL`, as well as the version, `16.6.0` (not stricly required, but good practise).
You select `URL` as source type and enter `https://cdn.jsdelivr.net/npm/graphql@16.6.0/+esm`.
Note that you can get open-source JavaScript modules like this one from the CDN of your choice as long as they are provided in terms of an EcmaScript module (ESM).

![](images/03-create-graphql-module.png " ")

What is left to do is to hit the "Create MLE Module" button and wait a few seconds to get the confirmation that the module was successfully created.

![](images/04-graphql-module-created.png " ")

## Task 3: Creating a GraphQL Schema for Book API

## Task 4: Combining fetch, GraphQL and SQL Driver to produce Book Service Results

## Task 5: Exposing Book Service as RESTFull Service

## Task 6: Creating Application for Book Service Consumption

## Task 7: Using Mustache to render Book Service Results

## **Summary**

You now know how to combine different external, community-provided JavaScript modules and use them in your APEX application or expose them as RESTFull service.

## **Learn More** - *Useful Links*

- [APEX on Autonomous](https://apex.oracle.com/autonomous)
- [APEX Collateral](https://www.oracle.com/database/technologies/appdev/apex/collateral.html)
- [Tutorials](https://apex.oracle.com/en/learn/tutorials)
- [Community](https://apex.oracle.com/community)
- [External Site + Slack](http://apex.world)

## **Acknowledgements**

 - **Author/Contributors** -  Lucas Braun, Principal Program Manager, Salim Hlayel, Principal Product Manager
 - **Last Updated By/Date** - Lucas Braun, Principal Program Manager, Salim Hlayel, Principal Product Manager, May 2023