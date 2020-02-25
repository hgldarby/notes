# The Pathologies of Big Data

- Big Data - extremely large data sets that may be analysed to reveal patterns
- Data inflation when unpacking the data, typical of traditional relational database management systems (RDBMS').
- Choice of algorithm is important for the size of data and the query used.
- PostgreSQL has more difficulty analysing the stored data than it does storing it.
- Truth about big data in traditional databases: it is easier to get data in than it is to get it out.
- The pathologies are primarily those of analysis.
- Data warehouse - "A copy of transaction data specifically structured for query and analysis."
- General approach for a data warehouse - commonly bulk extraction of the data from an operational database followed by reconstitution in a different database in a form more suitable for analytical queries (the so called "extract, transform, load" process)
- For big data, RDBMS based dimensional modeling and cube based OLAP(online analytical processing) were to slow or too limited.
- Most large datasets have temporal or spatial dimensions or both.
- Data with a time dimension should in most cases be stored and processed with at least a partial temporal ordering to preserve locality.
- Time-series analysis and forecasting aggregate data in an order-dependent manner.
- Hard limits in applications prove another challenge for data analysis.
- Linear vs random data access. Linear is far quicker 
- 