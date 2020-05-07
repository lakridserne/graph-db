# graph-db
:play movie graph

    // Newst movie release with Tom Hanks in it

A ) MATCH (tom:Person {name: 'Tom Hanks'})-[r:ACTED_IN]->(movie:Movie)
    WHERE movie.released > 2000
    RETURN tom, r, movie
    ORDER BY movie.released DESC
    
    
