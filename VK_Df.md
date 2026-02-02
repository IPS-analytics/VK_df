# VK_df
Creation of df for VK cloudgaming work 
 ```sql
CREATE TABLE "user" (
    user_id SERIAL PRIMARY KEY,
    registration_date DATE NOT NULL,
    country VARCHAR(10)
);

CREATE TABLE games (
    game_id SERIAL PRIMARY KEY,
    game_name VARCHAR(100)
);

CREATE TABLE sessions (
    session_id SERIAL PRIMARY KEY,
    user_id INT NOT NULL REFERENCES "user"(user_id),
    game_id INT NOT NULL REFERENCES games(game_id),
    session_start TIMESTAMP,
    session_end TIMESTAMP,
    session_status VARCHAR(20)
);

CREATE VIEW user_activities AS
SELECT
    u.user_id,
    u.registration_date,
    u.country,
    s.session_id,
    s.game_id,
    g.game_name,
    s.session_start,
    s.session_end,
    s.session_status
FROM sessions s
JOIN "user" u ON s.user_id = u.user_id
JOIN games g ON s.game_id = g.game_id;
select * 
from user_activities
```
