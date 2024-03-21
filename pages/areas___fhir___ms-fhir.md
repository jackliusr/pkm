- search-sql-server
  ```mermaid
  %%{init: {'theme': 'forest' } }%%
  sequenceDiagram
      SqlServerSearchService->>SearchInternalAsync: SearchOptions
      SearchInternalAsync->>SearchImpl: SearchOptions
      SearchImpl->>Expression: AcceptVisitor
      Expression->>SearchImpl: SqlRootExpression
      SearchImpl->>Expression: AcceptVisitor on SqlQueryGenerator w/ SearchOptions
      Expression->>SearchImpl: StringBuilder w/ SQL Command Text
      SearchImpl->>SqlCommand: ExecuteReader
      SqlCommand->>SearchImpl: SqlDataReader
      SearchImpl->>SqlDataReader: ReadRows
      SqlDataReader->>SearchImpl: RawResourceStream
      SearchImpl->>SearchInternalAsync: SearchResult (Constructed from RawResourceStream outputs)
      SearchInternalAsync->>SqlServerSearchService: SearchResult
  ```
- search-cosmos-db
  ```mermaid
  sequenceDiagram
      FhirCosmosSearchService->>SearchInternalAsync: SearchOptions
      SearchInternalAsync->>QueryBuilder: BuildSqlQuerySpec
      QueryBuilder->>QueryBuilderHelper: BuildSqlQuerySpec
      QueryBuilderHelper->>Expression: Accept Visitor
      Expression-->>QueryBuilderHelper: SqlQuerySpec
      QueryBuilderHelper-->>QueryBuilder: QueryDefinition
      QueryBuilder-->>SearchInternalAsync: SearchOptions
      SearchInternalAsync->>ExecuteSearchAsync: QueryDefinition
      ExecuteSearchAsync->>CosmosFhirDataStore: Execute Query on SQLQuerySpec
      CosmosFhirDataStore-->>ExecuteSearchAsync: FeedResponse
      ExecuteSearchAsync-->>SearchInternalAsync: SearchResult
      SearchInternalAsync-->>FhirCosmosSearchService: SearchResult
  ```