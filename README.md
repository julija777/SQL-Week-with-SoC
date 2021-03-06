# SQL-Week-with-SoC



**Schema (PostgreSQL v13)**

        CREATE TABLE users (
        user_id SERIAL PRIMARY KEY,
        first_name VARCHAR(15),
        last_name VARCHAR(15),
        email VARCHAR(30),
        dob DATE
    );
    
    CREATE TABLE posts (
        post_id SERIAL PRIMARY KEY,
        author INTEGER REFERENCES users(user_id),
        created timestamp not null default CURRENT_TIMESTAMP,
        content TEXT
    );
    
    CREATE TABLE comments (
        comment_id SERIAL PRIMARY KEY,
        post_id INTEGER REFERENCES posts(post_id),
        author INTEGER REFERENCES users(user_id),
        content TEXT,
        created timestamp not null default CURRENT_TIMESTAMP
    );
    
    INSERT INTO
        users (first_name, last_name, email, dob)
    VALUES
        (
            'Geoff',
            'Biggleswade',
            'g.biggle@gmail.com',
            '1992-09-01'
        ),
        (
            'Regina',
            'Clumpwitch',
            'r.clump@gmail.com',
            '1994-03-01'
        ),
        (
            'Sally',
            'Longmeadow',
            's.longmeadow@gmail.com',
            '1988-01-01'
        ),
        (
            'Frank',
            'Champion',
            'f.champ@gmail.com',
            '1972-01-09'
        ),
        (
            'Mella',
            'Capricious',
            'm.cap@gmail.com',
            '1980-03-03'
        ),
        (
            'Florence',
            'Dogsdinner',
            'f.dd@gmail.com',
            '1989-02-01'
        ),
        (
            'Wendy',
            'Prankmartin',
            'g.biggle@gmail.com',
            '1977-07-07'
        ),
        (
            'Sandy',
            'Earlsbottom',
            's.earlsbottom@gmail.com',
            '1961-01-01'
        ),
        (
            'Mandy',
            'Stevens',
            'g.biggle@gmail.com',
            '1982-12-12'
        );
    
    INSERT INTO
        posts (author, content)
    VALUES
        (
            1,
            'The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?!'
        ),
        (
            1,
            'Crisps are too yummy - prove me wrong.'
        ),
        (
            5,
            'I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!'
        );
    
    INSERT INTO
        comments (post_id, author, content)
    VALUES
        (
            1,
            2,
            'Yeh but have you given them to a dog? Makes them soo gentle.'
        ),
        (
            1,
            3,
            'I could not live without omelettes. Not so round after whisking, are they!!'
        ),
        (
            3,
            9,
            'YOU SAW THEM TOO!! They probed my husband'
        );
    

---

**Query #Everything in a table**

    select * from users;

| user_id | first_name | last_name   | email                   | dob                      |
| ------- | ---------- | ----------- | ----------------------- | ------------------------ |
| 1       | Geoff      | Biggleswade | g.biggle@gmail.com      | 1992-09-01T00:00:00.000Z |
| 2       | Regina     | Clumpwitch  | r.clump@gmail.com       | 1994-03-01T00:00:00.000Z |
| 3       | Sally      | Longmeadow  | s.longmeadow@gmail.com  | 1988-01-01T00:00:00.000Z |
| 4       | Frank      | Champion    | f.champ@gmail.com       | 1972-01-09T00:00:00.000Z |
| 5       | Mella      | Capricious  | m.cap@gmail.com         | 1980-03-03T00:00:00.000Z |
| 6       | Florence   | Dogsdinner  | f.dd@gmail.com          | 1989-02-01T00:00:00.000Z |
| 7       | Wendy      | Prankmartin | g.biggle@gmail.com      | 1977-07-07T00:00:00.000Z |
| 8       | Sandy      | Earlsbottom | s.earlsbottom@gmail.com | 1961-01-01T00:00:00.000Z |
| 9       | Mandy      | Stevens     | g.biggle@gmail.com      | 1982-12-12T00:00:00.000Z |

---
**Query #Everything in another table**

    select * from posts;

| post_id | author | created                  | content                                                                                               |
| ------- | ------ | ------------------------ | ----------------------------------------------------------------------------------------------------- |
| 1       | 1      | 2021-12-14T10:38:42.807Z | The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?! |
| 2       | 1      | 2021-12-14T10:38:42.807Z | Crisps are too yummy - prove me wrong.                                                                |
| 3       | 5      | 2021-12-14T10:38:42.807Z | I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!                  |

---
**Query #INNER JOIN**

    SELECT * FROM users
    INNER JOIN posts
    ON users.user_id = posts.author;

| user_id | first_name | last_name   | email              | dob                      | post_id | author | created                  | content                                                                                               |
| ------- | ---------- | ----------- | ------------------ | ------------------------ | ------- | ------ | ------------------------ | ----------------------------------------------------------------------------------------------------- |
| 1       | Geoff      | Biggleswade | g.biggle@gmail.com | 1992-09-01T00:00:00.000Z | 1       | 1      | 2021-12-14T10:38:42.807Z | The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?! |
| 1       | Geoff      | Biggleswade | g.biggle@gmail.com | 1992-09-01T00:00:00.000Z | 2       | 1      | 2021-12-14T10:38:42.807Z | Crisps are too yummy - prove me wrong.                                                                |
| 5       | Mella      | Capricious  | m.cap@gmail.com    | 1980-03-03T00:00:00.000Z | 3       | 5      | 2021-12-14T10:38:42.807Z | I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!                  |

---

[View on DB Fiddle](https://www.db-fiddle.com/f/uFaiUY5aSZkyKB5QdqegLE/0)

**Schema (PostgreSQL v13)**

        CREATE TABLE users (
        user_id SERIAL PRIMARY KEY,
        first_name VARCHAR(15),
        last_name VARCHAR(15),
        email VARCHAR(30),
        dob DATE
    );
    
    CREATE TABLE posts (
        post_id SERIAL PRIMARY KEY,
        author INTEGER REFERENCES users(user_id),
        created timestamp not null default CURRENT_TIMESTAMP,
        content TEXT
    );
    
    CREATE TABLE comments (
        comment_id SERIAL PRIMARY KEY,
        post_id INTEGER REFERENCES posts(post_id),
        author INTEGER REFERENCES users(user_id),
        content TEXT,
        created timestamp not null default CURRENT_TIMESTAMP
    );
    
    INSERT INTO
        users (first_name, last_name, email, dob)
    VALUES
        (
            'Geoff',
            'Biggleswade',
            'g.biggle@gmail.com',
            '1992-09-01'
        ),
        (
            'Regina',
            'Clumpwitch',
            'r.clump@gmail.com',
            '1994-03-01'
        ),
        (
            'Sally',
            'Longmeadow',
            's.longmeadow@gmail.com',
            '1988-01-01'
        ),
        (
            'Frank',
            'Champion',
            'f.champ@gmail.com',
            '1972-01-09'
        ),
        (
            'Mella',
            'Capricious',
            'm.cap@gmail.com',
            '1980-03-03'
        ),
        (
            'Florence',
            'Dogsdinner',
            'f.dd@gmail.com',
            '1989-02-01'
        ),
        (
            'Wendy',
            'Prankmartin',
            'g.biggle@gmail.com',
            '1977-07-07'
        ),
        (
            'Sandy',
            'Earlsbottom',
            's.earlsbottom@gmail.com',
            '1961-01-01'
        ),
        (
            'Mandy',
            'Stevens',
            'g.biggle@gmail.com',
            '1982-12-12'
        );
    
    INSERT INTO
        posts (author, content)
    VALUES
        (
            1,
            'The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?!'
        ),
        (
            1,
            'Crisps are too yummy - prove me wrong.'
        ),
        (
            5,
            'I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!'
        );
    
    INSERT INTO
        comments (post_id, author, content)
    VALUES
        (
            1,
            2,
            'Yeh but have you given them to a dog? Makes them soo gentle.'
        ),
        (
            1,
            3,
            'I could not live without omelettes. Not so round after whisking, are they!!'
        ),
        (
            3,
            9,
            'YOU SAW THEM TOO!! They probed my husband'
        );
    

---

**Query #INNER JOIN**

    SELECT *
    FROM comments 
    INNER JOIN users
    ON comments.author = users.user_id;

| comment_id | post_id | author | content                                                                     | created                  | user_id | first_name | last_name  | email                  | dob                      |
| ---------- | ------- | ------ | --------------------------------------------------------------------------- | ------------------------ | ------- | ---------- | ---------- | ---------------------- | ------------------------ |
| 1          | 1       | 2      | Yeh but have you given them to a dog? Makes them soo gentle.                | 2021-12-14T10:42:59.861Z | 2       | Regina     | Clumpwitch | r.clump@gmail.com      | 1994-03-01T00:00:00.000Z |
| 2          | 1       | 3      | I could not live without omelettes. Not so round after whisking, are they!! | 2021-12-14T10:42:59.861Z | 3       | Sally      | Longmeadow | s.longmeadow@gmail.com | 1988-01-01T00:00:00.000Z |
| 3          | 3       | 9      | YOU SAW THEM TOO!! They probed my husband                                   | 2021-12-14T10:42:59.861Z | 9       | Mandy      | Stevens    | g.biggle@gmail.com     | 1982-12-12T00:00:00.000Z |

---

[View on DB Fiddle](https://www.db-fiddle.com/f/uFaiUY5aSZkyKB5QdqegLE/0)


**Schema (PostgreSQL v13)**

        CREATE TABLE users (
        user_id SERIAL PRIMARY KEY,
        first_name VARCHAR(15),
        last_name VARCHAR(15),
        email VARCHAR(30),
        dob DATE
    );
    
    CREATE TABLE posts (
        post_id SERIAL PRIMARY KEY,
        author INTEGER REFERENCES users(user_id),
        created timestamp not null default CURRENT_TIMESTAMP,
        content TEXT
    );
    
    CREATE TABLE comments (
        comment_id SERIAL PRIMARY KEY,
        post_id INTEGER REFERENCES posts(post_id),
        author INTEGER REFERENCES users(user_id),
        content TEXT,
        created timestamp not null default CURRENT_TIMESTAMP
    );
    
    INSERT INTO
        users (first_name, last_name, email, dob)
    VALUES
        (
            'Geoff',
            'Biggleswade',
            'g.biggle@gmail.com',
            '1992-09-01'
        ),
        (
            'Regina',
            'Clumpwitch',
            'r.clump@gmail.com',
            '1994-03-01'
        ),
        (
            'Sally',
            'Longmeadow',
            's.longmeadow@gmail.com',
            '1988-01-01'
        ),
        (
            'Frank',
            'Champion',
            'f.champ@gmail.com',
            '1972-01-09'
        ),
        (
            'Mella',
            'Capricious',
            'm.cap@gmail.com',
            '1980-03-03'
        ),
        (
            'Florence',
            'Dogsdinner',
            'f.dd@gmail.com',
            '1989-02-01'
        ),
        (
            'Wendy',
            'Prankmartin',
            'g.biggle@gmail.com',
            '1977-07-07'
        ),
        (
            'Sandy',
            'Earlsbottom',
            's.earlsbottom@gmail.com',
            '1961-01-01'
        ),
        (
            'Mandy',
            'Stevens',
            'g.biggle@gmail.com',
            '1982-12-12'
        );
    
    INSERT INTO
        posts (author, content)
    VALUES
        (
            1,
            'The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?!'
        ),
        (
            1,
            'Crisps are too yummy - prove me wrong.'
        ),
        (
            5,
            'I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!'
        );
    
    INSERT INTO
        comments (post_id, author, content)
    VALUES
        (
            1,
            2,
            'Yeh but have you given them to a dog? Makes them soo gentle.'
        ),
        (
            1,
            3,
            'I could not live without omelettes. Not so round after whisking, are they!!'
        ),
        (
            3,
            9,
            'YOU SAW THEM TOO!! They probed my husband'
        );
    

---

**Query #LEFT JOIN**

    SELECT *
    FROM users
    LEFT JOIN posts
    on users.user_id = posts.author;

| user_id | first_name | last_name   | email                   | dob                      | post_id | author | created                  | content                                                                                               |
| ------- | ---------- | ----------- | ----------------------- | ------------------------ | ------- | ------ | ------------------------ | ----------------------------------------------------------------------------------------------------- |
| 1       | Geoff      | Biggleswade | g.biggle@gmail.com      | 1992-09-01T00:00:00.000Z | 1       | 1      | 2021-12-14T10:54:23.455Z | The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?! |
| 1       | Geoff      | Biggleswade | g.biggle@gmail.com      | 1992-09-01T00:00:00.000Z | 2       | 1      | 2021-12-14T10:54:23.455Z | Crisps are too yummy - prove me wrong.                                                                |
| 5       | Mella      | Capricious  | m.cap@gmail.com         | 1980-03-03T00:00:00.000Z | 3       | 5      | 2021-12-14T10:54:23.455Z | I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!                  |
| 2       | Regina     | Clumpwitch  | r.clump@gmail.com       | 1994-03-01T00:00:00.000Z |         |        |                          |                                                                                                       |
| 8       | Sandy      | Earlsbottom | s.earlsbottom@gmail.com | 1961-01-01T00:00:00.000Z |         |        |                          |                                                                                                       |
| 6       | Florence   | Dogsdinner  | f.dd@gmail.com          | 1989-02-01T00:00:00.000Z |         |        |                          |                                                                                                       |
| 4       | Frank      | Champion    | f.champ@gmail.com       | 1972-01-09T00:00:00.000Z |         |        |                          |                                                                                                       |
| 3       | Sally      | Longmeadow  | s.longmeadow@gmail.com  | 1988-01-01T00:00:00.000Z |         |        |                          |                                                                                                       |
| 9       | Mandy      | Stevens     | g.biggle@gmail.com      | 1982-12-12T00:00:00.000Z |         |        |                          |                                                                                                       |
| 7       | Wendy      | Prankmartin | g.biggle@gmail.com      | 1977-07-07T00:00:00.000Z |         |        |                          |                                                                                                       |

---

[View on DB Fiddle](https://www.db-fiddle.com/f/uFaiUY5aSZkyKB5QdqegLE/0)

**Schema (PostgreSQL v13)**

        CREATE TABLE users (
        user_id SERIAL PRIMARY KEY,
        first_name VARCHAR(15),
        last_name VARCHAR(15),
        email VARCHAR(30),
        dob DATE
    );
    
    CREATE TABLE posts (
        post_id SERIAL PRIMARY KEY,
        author INTEGER REFERENCES users(user_id),
        created timestamp not null default CURRENT_TIMESTAMP,
        content TEXT
    );
    
    CREATE TABLE comments (
        comment_id SERIAL PRIMARY KEY,
        post_id INTEGER REFERENCES posts(post_id),
        author INTEGER REFERENCES users(user_id),
        content TEXT,
        created timestamp not null default CURRENT_TIMESTAMP
    );
    
    INSERT INTO
        users (first_name, last_name, email, dob)
    VALUES
        (
            'Geoff',
            'Biggleswade',
            'g.biggle@gmail.com',
            '1992-09-01'
        ),
        (
            'Regina',
            'Clumpwitch',
            'r.clump@gmail.com',
            '1994-03-01'
        ),
        (
            'Sally',
            'Longmeadow',
            's.longmeadow@gmail.com',
            '1988-01-01'
        ),
        (
            'Frank',
            'Champion',
            'f.champ@gmail.com',
            '1972-01-09'
        ),
        (
            'Mella',
            'Capricious',
            'm.cap@gmail.com',
            '1980-03-03'
        ),
        (
            'Florence',
            'Dogsdinner',
            'f.dd@gmail.com',
            '1989-02-01'
        ),
        (
            'Wendy',
            'Prankmartin',
            'g.biggle@gmail.com',
            '1977-07-07'
        ),
        (
            'Sandy',
            'Earlsbottom',
            's.earlsbottom@gmail.com',
            '1961-01-01'
        ),
        (
            'Mandy',
            'Stevens',
            'g.biggle@gmail.com',
            '1982-12-12'
        );
    
    INSERT INTO
        posts (author, content)
    VALUES
        (
            1,
            'The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?!'
        ),
        (
            1,
            'Crisps are too yummy - prove me wrong.'
        ),
        (
            5,
            'I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!'
        );
    
    INSERT INTO
        comments (post_id, author, content)
    VALUES
        (
            1,
            2,
            'Yeh but have you given them to a dog? Makes them soo gentle.'
        ),
        (
            1,
            3,
            'I could not live without omelettes. Not so round after whisking, are they!!'
        ),
        (
            3,
            9,
            'YOU SAW THEM TOO!! They probed my husband'
        );
    

---

**Query #LEFT JOIN**

    SELECT *
    FROM users
    LEFT JOIN comments
    on users.user_id = comments.author;

| user_id | first_name | last_name   | email                   | dob                      | comment_id | post_id | author | content                                                                     | created                  |
| ------- | ---------- | ----------- | ----------------------- | ------------------------ | ---------- | ------- | ------ | --------------------------------------------------------------------------- | ------------------------ |
| 2       | Regina     | Clumpwitch  | r.clump@gmail.com       | 1994-03-01T00:00:00.000Z | 1          | 1       | 2      | Yeh but have you given them to a dog? Makes them soo gentle.                | 2021-12-14T10:56:01.504Z |
| 3       | Sally      | Longmeadow  | s.longmeadow@gmail.com  | 1988-01-01T00:00:00.000Z | 2          | 1       | 3      | I could not live without omelettes. Not so round after whisking, are they!! | 2021-12-14T10:56:01.504Z |
| 9       | Mandy      | Stevens     | g.biggle@gmail.com      | 1982-12-12T00:00:00.000Z | 3          | 3       | 9      | YOU SAW THEM TOO!! They probed my husband                                   | 2021-12-14T10:56:01.504Z |
| 5       | Mella      | Capricious  | m.cap@gmail.com         | 1980-03-03T00:00:00.000Z |            |         |        |                                                                             |                          |
| 8       | Sandy      | Earlsbottom | s.earlsbottom@gmail.com | 1961-01-01T00:00:00.000Z |            |         |        |                                                                             |                          |
| 6       | Florence   | Dogsdinner  | f.dd@gmail.com          | 1989-02-01T00:00:00.000Z |            |         |        |                                                                             |                          |
| 4       | Frank      | Champion    | f.champ@gmail.com       | 1972-01-09T00:00:00.000Z |            |         |        |                                                                             |                          |
| 1       | Geoff      | Biggleswade | g.biggle@gmail.com      | 1992-09-01T00:00:00.000Z |            |         |        |                                                                             |                          |
| 7       | Wendy      | Prankmartin | g.biggle@gmail.com      | 1977-07-07T00:00:00.000Z |            |         |        |                                                                             |                          |

---

[View on DB Fiddle](https://www.db-fiddle.com/f/uFaiUY5aSZkyKB5QdqegLE/0)

**Schema (PostgreSQL v13)**

        CREATE TABLE users (
        user_id SERIAL PRIMARY KEY,
        first_name VARCHAR(15),
        last_name VARCHAR(15),
        email VARCHAR(30),
        dob DATE
    );
    
    CREATE TABLE posts (
        post_id SERIAL PRIMARY KEY,
        author INTEGER REFERENCES users(user_id),
        created timestamp not null default CURRENT_TIMESTAMP,
        content TEXT
    );
    
    CREATE TABLE comments (
        comment_id SERIAL PRIMARY KEY,
        post_id INTEGER REFERENCES posts(post_id),
        author INTEGER REFERENCES users(user_id),
        content TEXT,
        created timestamp not null default CURRENT_TIMESTAMP
    );
    
    INSERT INTO
        users (first_name, last_name, email, dob)
    VALUES
        (
            'Geoff',
            'Biggleswade',
            'g.biggle@gmail.com',
            '1992-09-01'
        ),
        (
            'Regina',
            'Clumpwitch',
            'r.clump@gmail.com',
            '1994-03-01'
        ),
        (
            'Sally',
            'Longmeadow',
            's.longmeadow@gmail.com',
            '1988-01-01'
        ),
        (
            'Frank',
            'Champion',
            'f.champ@gmail.com',
            '1972-01-09'
        ),
        (
            'Mella',
            'Capricious',
            'm.cap@gmail.com',
            '1980-03-03'
        ),
        (
            'Florence',
            'Dogsdinner',
            'f.dd@gmail.com',
            '1989-02-01'
        ),
        (
            'Wendy',
            'Prankmartin',
            'g.biggle@gmail.com',
            '1977-07-07'
        ),
        (
            'Sandy',
            'Earlsbottom',
            's.earlsbottom@gmail.com',
            '1961-01-01'
        ),
        (
            'Mandy',
            'Stevens',
            'g.biggle@gmail.com',
            '1982-12-12'
        );
    
    INSERT INTO
        posts (author, content)
    VALUES
        (
            1,
            'The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?!'
        ),
        (
            1,
            'Crisps are too yummy - prove me wrong.'
        ),
        (
            5,
            'I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!'
        );
    
    INSERT INTO
        comments (post_id, author, content)
    VALUES
        (
            1,
            2,
            'Yeh but have you given them to a dog? Makes them soo gentle.'
        ),
        (
            1,
            3,
            'I could not live without omelettes. Not so round after whisking, are they!!'
        ),
        (
            3,
            9,
            'YOU SAW THEM TOO!! They probed my husband'
        );
    

---

**Query #LEFT JOIN**

    SELECT posts.content, comments.content
    FROM posts
    LEFT JOIN comments
    ON posts.post_id = comments.post_id;

| content                                                                                               | content                                                                     |
| ----------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?! | Yeh but have you given them to a dog? Makes them soo gentle.                |
| The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?! | I could not live without omelettes. Not so round after whisking, are they!! |
| I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!                  | YOU SAW THEM TOO!! They probed my husband                                   |
| Crisps are too yummy - prove me wrong.                                                                |                                                                             |

---

[View on DB Fiddle](https://www.db-fiddle.com/f/uFaiUY5aSZkyKB5QdqegLE/0)

**Schema (PostgreSQL v13)**

        CREATE TABLE users (
        user_id SERIAL PRIMARY KEY,
        first_name VARCHAR(15),
        last_name VARCHAR(15),
        email VARCHAR(30),
        dob DATE
    );
    
    CREATE TABLE posts (
        post_id SERIAL PRIMARY KEY,
        author INTEGER REFERENCES users(user_id),
        created timestamp not null default CURRENT_TIMESTAMP,
        content TEXT
    );
    
    CREATE TABLE comments (
        comment_id SERIAL PRIMARY KEY,
        post_id INTEGER REFERENCES posts(post_id),
        author INTEGER REFERENCES users(user_id),
        content TEXT,
        created timestamp not null default CURRENT_TIMESTAMP
    );
    
    INSERT INTO
        users (first_name, last_name, email, dob)
    VALUES
        (
            'Geoff',
            'Biggleswade',
            'g.biggle@gmail.com',
            '1992-09-01'
        ),
        (
            'Regina',
            'Clumpwitch',
            'r.clump@gmail.com',
            '1994-03-01'
        ),
        (
            'Sally',
            'Longmeadow',
            's.longmeadow@gmail.com',
            '1988-01-01'
        ),
        (
            'Frank',
            'Champion',
            'f.champ@gmail.com',
            '1972-01-09'
        ),
        (
            'Mella',
            'Capricious',
            'm.cap@gmail.com',
            '1980-03-03'
        ),
        (
            'Florence',
            'Dogsdinner',
            'f.dd@gmail.com',
            '1989-02-01'
        ),
        (
            'Wendy',
            'Prankmartin',
            'g.biggle@gmail.com',
            '1977-07-07'
        ),
        (
            'Sandy',
            'Earlsbottom',
            's.earlsbottom@gmail.com',
            '1961-01-01'
        ),
        (
            'Mandy',
            'Stevens',
            'g.biggle@gmail.com',
            '1982-12-12'
        );
    
    INSERT INTO
        posts (author, content)
    VALUES
        (
            1,
            'The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?!'
        ),
        (
            1,
            'Crisps are too yummy - prove me wrong.'
        ),
        (
            5,
            'I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!'
        );
    
    INSERT INTO
        comments (post_id, author, content)
    VALUES
        (
            1,
            2,
            'Yeh but have you given them to a dog? Makes them soo gentle.'
        ),
        (
            1,
            3,
            'I could not live without omelettes. Not so round after whisking, are they!!'
        ),
        (
            3,
            9,
            'YOU SAW THEM TOO!! They probed my husband'
        );
    

---

**Query #RIGHT JOIN**

    SELECT *
        FROM comments
        RIGHT JOIN users
        on comments.author = users.user_id;

| comment_id | post_id | author | content                                                                     | created                  | user_id | first_name | last_name   | email                   | dob                      |
| ---------- | ------- | ------ | --------------------------------------------------------------------------- | ------------------------ | ------- | ---------- | ----------- | ----------------------- | ------------------------ |
| 1          | 1       | 2      | Yeh but have you given them to a dog? Makes them soo gentle.                | 2021-12-14T11:24:14.176Z | 2       | Regina     | Clumpwitch  | r.clump@gmail.com       | 1994-03-01T00:00:00.000Z |
| 2          | 1       | 3      | I could not live without omelettes. Not so round after whisking, are they!! | 2021-12-14T11:24:14.176Z | 3       | Sally      | Longmeadow  | s.longmeadow@gmail.com  | 1988-01-01T00:00:00.000Z |
| 3          | 3       | 9      | YOU SAW THEM TOO!! They probed my husband                                   | 2021-12-14T11:24:14.176Z | 9       | Mandy      | Stevens     | g.biggle@gmail.com      | 1982-12-12T00:00:00.000Z |
|            |         |        |                                                                             |                          | 5       | Mella      | Capricious  | m.cap@gmail.com         | 1980-03-03T00:00:00.000Z |
|            |         |        |                                                                             |                          | 8       | Sandy      | Earlsbottom | s.earlsbottom@gmail.com | 1961-01-01T00:00:00.000Z |
|            |         |        |                                                                             |                          | 6       | Florence   | Dogsdinner  | f.dd@gmail.com          | 1989-02-01T00:00:00.000Z |
|            |         |        |                                                                             |                          | 4       | Frank      | Champion    | f.champ@gmail.com       | 1972-01-09T00:00:00.000Z |
|            |         |        |                                                                             |                          | 1       | Geoff      | Biggleswade | g.biggle@gmail.com      | 1992-09-01T00:00:00.000Z |
|            |         |        |                                                                             |                          | 7       | Wendy      | Prankmartin | g.biggle@gmail.com      | 1977-07-07T00:00:00.000Z |

---

[View on DB Fiddle](https://www.db-fiddle.com/f/uFaiUY5aSZkyKB5QdqegLE/0)

**Schema (PostgreSQL v13)**

        CREATE TABLE users (
        user_id SERIAL PRIMARY KEY,
        first_name VARCHAR(15),
        last_name VARCHAR(15),
        email VARCHAR(30),
        dob DATE
    );
    
    CREATE TABLE posts (
        post_id SERIAL PRIMARY KEY,
        author INTEGER REFERENCES users(user_id),
        created timestamp not null default CURRENT_TIMESTAMP,
        content TEXT
    );
    
    CREATE TABLE comments (
        comment_id SERIAL PRIMARY KEY,
        post_id INTEGER REFERENCES posts(post_id),
        author INTEGER REFERENCES users(user_id),
        content TEXT,
        created timestamp not null default CURRENT_TIMESTAMP
    );
    
    INSERT INTO
        users (first_name, last_name, email, dob)
    VALUES
        (
            'Geoff',
            'Biggleswade',
            'g.biggle@gmail.com',
            '1992-09-01'
        ),
        (
            'Regina',
            'Clumpwitch',
            'r.clump@gmail.com',
            '1994-03-01'
        ),
        (
            'Sally',
            'Longmeadow',
            's.longmeadow@gmail.com',
            '1988-01-01'
        ),
        (
            'Frank',
            'Champion',
            'f.champ@gmail.com',
            '1972-01-09'
        ),
        (
            'Mella',
            'Capricious',
            'm.cap@gmail.com',
            '1980-03-03'
        ),
        (
            'Florence',
            'Dogsdinner',
            'f.dd@gmail.com',
            '1989-02-01'
        ),
        (
            'Wendy',
            'Prankmartin',
            'g.biggle@gmail.com',
            '1977-07-07'
        ),
        (
            'Sandy',
            'Earlsbottom',
            's.earlsbottom@gmail.com',
            '1961-01-01'
        ),
        (
            'Mandy',
            'Stevens',
            'g.biggle@gmail.com',
            '1982-12-12'
        );
    
    INSERT INTO
        posts (author, content)
    VALUES
        (
            1,
            'The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?!'
        ),
        (
            1,
            'Crisps are too yummy - prove me wrong.'
        ),
        (
            5,
            'I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!'
        );
    
    INSERT INTO
        comments (post_id, author, content)
    VALUES
        (
            1,
            2,
            'Yeh but have you given them to a dog? Makes them soo gentle.'
        ),
        (
            1,
            3,
            'I could not live without omelettes. Not so round after whisking, are they!!'
        ),
        (
            3,
            9,
            'YOU SAW THEM TOO!! They probed my husband'
        );
    

---

**Query #RIGHT JOIN**

    SELECT first_name, last_name, content
        FROM posts
        RIGHT JOIN users
        on posts.author = users.user_id;

| first_name | last_name   | content                                                                                               |
| ---------- | ----------- | ----------------------------------------------------------------------------------------------------- |
| Geoff      | Biggleswade | The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?! |
| Geoff      | Biggleswade | Crisps are too yummy - prove me wrong.                                                                |
| Mella      | Capricious  | I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!                  |
| Regina     | Clumpwitch  |                                                                                                       |
| Sandy      | Earlsbottom |                                                                                                       |
| Florence   | Dogsdinner  |                                                                                                       |
| Frank      | Champion    |                                                                                                       |
| Sally      | Longmeadow  |                                                                                                       |
| Mandy      | Stevens     |                                                                                                       |
| Wendy      | Prankmartin |                                                                                                       |

---

[View on DB Fiddle](https://www.db-fiddle.com/f/uFaiUY5aSZkyKB5QdqegLE/0)


**Schema (PostgreSQL v13)**

        CREATE TABLE users (
        user_id SERIAL PRIMARY KEY,
        first_name VARCHAR(15),
        last_name VARCHAR(15),
        email VARCHAR(30),
        dob DATE
    );
    
    CREATE TABLE posts (
        post_id SERIAL PRIMARY KEY,
        author INTEGER REFERENCES users(user_id),
        created timestamp not null default CURRENT_TIMESTAMP,
        content TEXT
    );
    
    CREATE TABLE comments (
        comment_id SERIAL PRIMARY KEY,
        post_id INTEGER REFERENCES posts(post_id),
        author INTEGER REFERENCES users(user_id),
        content TEXT,
        created timestamp not null default CURRENT_TIMESTAMP
    );
    
    INSERT INTO
        users (first_name, last_name, email, dob)
    VALUES
        (
            'Geoff',
            'Biggleswade',
            'g.biggle@gmail.com',
            '1992-09-01'
        ),
        (
            'Regina',
            'Clumpwitch',
            'r.clump@gmail.com',
            '1994-03-01'
        ),
        (
            'Sally',
            'Longmeadow',
            's.longmeadow@gmail.com',
            '1988-01-01'
        ),
        (
            'Frank',
            'Champion',
            'f.champ@gmail.com',
            '1972-01-09'
        ),
        (
            'Mella',
            'Capricious',
            'm.cap@gmail.com',
            '1980-03-03'
        ),
        (
            'Florence',
            'Dogsdinner',
            'f.dd@gmail.com',
            '1989-02-01'
        ),
        (
            'Wendy',
            'Prankmartin',
            'g.biggle@gmail.com',
            '1977-07-07'
        ),
        (
            'Sandy',
            'Earlsbottom',
            's.earlsbottom@gmail.com',
            '1961-01-01'
        ),
        (
            'Mandy',
            'Stevens',
            'g.biggle@gmail.com',
            '1982-12-12'
        );
    
    INSERT INTO
        posts (author, content)
    VALUES
        (
            1,
            'The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?!'
        ),
        (
            1,
            'Crisps are too yummy - prove me wrong.'
        ),
        (
            5,
            'I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!'
        );
    
    INSERT INTO
        comments (post_id, author, content)
    VALUES
        (
            1,
            2,
            'Yeh but have you given them to a dog? Makes them soo gentle.'
        ),
        (
            1,
            3,
            'I could not live without omelettes. Not so round after whisking, are they!!'
        ),
        (
            3,
            9,
            'YOU SAW THEM TOO!! They probed my husband'
        );
    

---

**Query #FULL JOIN**

    SELECT *
        FROM posts
        FULL JOIN users
        on posts.author = users.user_id;

| post_id | author | created                  | content                                                                                               | user_id | first_name | last_name   | email                   | dob                      |
| ------- | ------ | ------------------------ | ----------------------------------------------------------------------------------------------------- | ------- | ---------- | ----------- | ----------------------- | ------------------------ |
| 1       | 1      | 2021-12-14T11:28:52.371Z | The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?! | 1       | Geoff      | Biggleswade | g.biggle@gmail.com      | 1992-09-01T00:00:00.000Z |
| 2       | 1      | 2021-12-14T11:28:52.371Z | Crisps are too yummy - prove me wrong.                                                                | 1       | Geoff      | Biggleswade | g.biggle@gmail.com      | 1992-09-01T00:00:00.000Z |
| 3       | 5      | 2021-12-14T11:28:52.371Z | I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!                  | 5       | Mella      | Capricious  | m.cap@gmail.com         | 1980-03-03T00:00:00.000Z |
|         |        |                          |                                                                                                       | 2       | Regina     | Clumpwitch  | r.clump@gmail.com       | 1994-03-01T00:00:00.000Z |
|         |        |                          |                                                                                                       | 8       | Sandy      | Earlsbottom | s.earlsbottom@gmail.com | 1961-01-01T00:00:00.000Z |
|         |        |                          |                                                                                                       | 6       | Florence   | Dogsdinner  | f.dd@gmail.com          | 1989-02-01T00:00:00.000Z |
|         |        |                          |                                                                                                       | 4       | Frank      | Champion    | f.champ@gmail.com       | 1972-01-09T00:00:00.000Z |
|         |        |                          |                                                                                                       | 3       | Sally      | Longmeadow  | s.longmeadow@gmail.com  | 1988-01-01T00:00:00.000Z |
|         |        |                          |                                                                                                       | 9       | Mandy      | Stevens     | g.biggle@gmail.com      | 1982-12-12T00:00:00.000Z |
|         |        |                          |                                                                                                       | 7       | Wendy      | Prankmartin | g.biggle@gmail.com      | 1977-07-07T00:00:00.000Z |

---

[View on DB Fiddle](https://www.db-fiddle.com/f/uFaiUY5aSZkyKB5QdqegLE/0)

**Schema (PostgreSQL v13)**

        CREATE TABLE users (
        user_id SERIAL PRIMARY KEY,
        first_name VARCHAR(15),
        last_name VARCHAR(15),
        email VARCHAR(30),
        dob DATE
    );
    
    CREATE TABLE posts (
        post_id SERIAL PRIMARY KEY,
        author INTEGER REFERENCES users(user_id),
        created timestamp not null default CURRENT_TIMESTAMP,
        content TEXT
    );
    
    CREATE TABLE comments (
        comment_id SERIAL PRIMARY KEY,
        post_id INTEGER REFERENCES posts(post_id),
        author INTEGER REFERENCES users(user_id),
        content TEXT,
        created timestamp not null default CURRENT_TIMESTAMP
    );
    
    INSERT INTO
        users (first_name, last_name, email, dob)
    VALUES
        (
            'Geoff',
            'Biggleswade',
            'g.biggle@gmail.com',
            '1992-09-01'
        ),
        (
            'Regina',
            'Clumpwitch',
            'r.clump@gmail.com',
            '1994-03-01'
        ),
        (
            'Sally',
            'Longmeadow',
            's.longmeadow@gmail.com',
            '1988-01-01'
        ),
        (
            'Frank',
            'Champion',
            'f.champ@gmail.com',
            '1972-01-09'
        ),
        (
            'Mella',
            'Capricious',
            'm.cap@gmail.com',
            '1980-03-03'
        ),
        (
            'Florence',
            'Dogsdinner',
            'f.dd@gmail.com',
            '1989-02-01'
        ),
        (
            'Wendy',
            'Prankmartin',
            'g.biggle@gmail.com',
            '1977-07-07'
        ),
        (
            'Sandy',
            'Earlsbottom',
            's.earlsbottom@gmail.com',
            '1961-01-01'
        ),
        (
            'Mandy',
            'Stevens',
            'g.biggle@gmail.com',
            '1982-12-12'
        );
    
    INSERT INTO
        posts (author, content)
    VALUES
        (
            1,
            'The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?!'
        ),
        (
            1,
            'Crisps are too yummy - prove me wrong.'
        ),
        (
            5,
            'I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!'
        );
    
    INSERT INTO
        comments (post_id, author, content)
    VALUES
        (
            1,
            2,
            'Yeh but have you given them to a dog? Makes them soo gentle.'
        ),
        (
            1,
            3,
            'I could not live without omelettes. Not so round after whisking, are they!!'
        ),
        (
            3,
            9,
            'YOU SAW THEM TOO!! They probed my husband'
        );
    

---

**Query #FULL JOIN**

    SELECT *
        FROM posts
        FULL JOIN comments
        on comments.post_id = posts.post_id;

| post_id | author | created                  | content                                                                                               | comment_id | post_id | author | content                                                                     | created                  |
| ------- | ------ | ------------------------ | ----------------------------------------------------------------------------------------------------- | ---------- | ------- | ------ | --------------------------------------------------------------------------- | ------------------------ |
| 1       | 1      | 2021-12-14T11:30:04.438Z | The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?! | 1          | 1       | 2      | Yeh but have you given them to a dog? Makes them soo gentle.                | 2021-12-14T11:30:04.439Z |
| 1       | 1      | 2021-12-14T11:30:04.438Z | The trouble with eggs is that they are somewhere between too round and not round enough. Am I right?! | 2          | 1       | 3      | I could not live without omelettes. Not so round after whisking, are they!! | 2021-12-14T11:30:04.439Z |
| 3       | 5      | 2021-12-14T11:30:04.438Z | I seen ALIENS! Green/silver sky lights above the A38 on tuesday. Watch out poeple!!!                  | 3          | 3       | 9      | YOU SAW THEM TOO!! They probed my husband                                   | 2021-12-14T11:30:04.439Z |
| 2       | 1      | 2021-12-14T11:30:04.438Z | Crisps are too yummy - prove me wrong.                                                                |            |         |        |                                                                             |                          |

---

[View on DB Fiddle](https://www.db-fiddle.com/f/uFaiUY5aSZkyKB5QdqegLE/0)
