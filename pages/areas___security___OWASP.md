- Application Security Verification Standard (ASVS)
- Reflected File Download(RFD): a web attack vector that enables attackers to gain complete control over a victims machine by virtually downloading a file from a trusted domain.
- top 10:
	- Missing Function Level Access Control
	  collapsed:: true
		- Mitigation Techniques
			- Use deny by default principle
			- Use least privilege principle
			- Validate the permissions on every request
			- Do not rely on hidden URLs or APIs
	- Plain Text Storage of Passwords
		- Cryptographic hashes vs password hashes
		- Mitigation Techniques
			- Use password hashing instead of password encryption
			- Choose an appropriate password hashing algorithm: PBKDF2
				- Argon2
				- bcrypt
				- PBKDF2
				- scrypt
			- Choose an appropriate configuration for Salting, Peppering and Work Factors
				- Work Factors: essentially the number of iterations of the hashing algorithm that are performed for each password.
					- `Argon2id`: has three different parameters that can be configured to adjust the work factor. (m) minimum memory size, (t) minimum number of iterations, and (p) the degree of parallelism. The following configuration settings represent a base minimum:
						- Option 1: m=37, t=1, p=1
						- Option 2: m=15, t=2, p=1
					- `bcrypt`: the work factor should be as large as verification server performance will allow, with a minimum of 10.
					- `PBKDF2`: the work factor for PBKDF2 is implemented through an iteration count, which should be set differently based on the internal hashing algorithm used:
						- PBKDF2-HMAC-SHA1: 720,000 iterations
						- PBKDF2-HMAC-SHA256: 310,000 iterations
						- PBKDF2-HMAC-SHA512: 120,000 iterations
	- SQL injection
		- Some common types of SQL injection attacks
			- `Tautology attacks`: These attacks involve injecting a tautology, or a logical statement that is always true, into a query to bypass authentication or access restricted data.
			  ```sql
			  select * from account where id={a} or 1=1; --
			  ```
			- `Union-based attacks`: These attacks involve injecting a UNION operator into a query to combine the results of multiple queries, potentially allowing the attacker to access data from multiple tables or databases.
			- `Error-based attacks`: These attacks involve injecting syntax errors or other invalid input into a query to cause the database to generate error messages, which can reveal sensitive information about the structure or content of the database.
			- `Blind SQL injection attacks`: These attacks involve injecting input into a query that causes the database to perform a specific action, such as a delay or a change in output, without revealing the results of the query. This type of attack can be more difficult to detect as it does not generate error messages or other visible signs of compromise.
			- `Inferential SQL injection attacks`: These attacks involve injecting input into a query that causes the database to perform a specific action, such as a delay or a change in output, which the attacker can observe and use to infer the results of the query. This type of attack can be used to extract sensitive information from a database without revealing the results of the query.
			- `Second-order SQL injection attacks`: Occurs when an attacker can insert malicious data into a database and then subsequently cause the application to retrieve and execute that malicious data as if it were a legitimate SQL statement.
		- Mitigation Techniques
		  collapsed:: true
			- Use of prepared statements with parameterized queries
			- Use parameterized stored procedures
			- Validating and sanitizing user input
	- Insufficient Validation