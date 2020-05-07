# graph-db
:play movie graph

    // Newst movie release with Tom Hanks in it

A ) MATCH (tom:Person {name: 'Tom Hanks'})-[r:ACTED_IN]->(movie:Movie)
    WHERE movie.released > 2000
    RETURN tom, r, movie
    ORDER BY movie.released DESC
    
    
    // Import cvs file
```
LOAD CSV WITH HEADERS FROM 'file:///C:/Users/Gordon/.Neo4jDesktop/neo4jDatabases/database-71774c0f-66c4-4247-a9e1-576ff0f9d2d9/installation-3.5.17/import/character-deaths.csv' as row
WITH row WHERE row.`Book of Death` IS NOT NULL
MATCH (p:Person)
WHERE p.id = replace(row.Name,' ','-')
SET p.death_book = toInteger(row.`Book of Death`)
```


b)
```
CALL gds.louvain.stream(
  // Filter out only person who
  // interacted in the first book
  'MATCH (p:Person)
  WHERE (p)-[:INTERACTS_1]-()
  RETURN id(p) as id'
  ,
  'MATCH (p:Person)-[:INTERACTS_1]-(p1:Person)
   RETURN id(p) as source, id(p1) as target'
  ,{graph:'cypher', direction:'BOTH', writeProperty:'community_1'})   
  ```
