User
----
id (PK)
name
password
email
is_guest
created_at
updated_at

Station
-------
station_id (PK)
station_name
station_code

Route
-----
route_id (PK)
departure_station_id (FK -> Station.station_id)
arrival_station_id (FK -> Station.station_id)
route_name

Schedule
--------
schedule_id (PK)
train_type
route_id (FK -> Route.route_id)
departure_time
arrival_time
price

StationRegistrationHistory
--------------------------
history_id (PK)
user_id (FK -> User.id)
route_id (FK -> Route.route_id)
registered_at
price


erDiagram
    User {
        INTEGER id PK
        VARCHAR name
        VARCHAR password
        VARCHAR email
        BOOLEAN is_guest
        TIMESTAMP created_at
        TIMESTAMP updated_at
    }

    Station {
        INTEGER station_id PK
        VARCHAR station_name
        VARCHAR station_code
    }

    Route {
        INTEGER route_id PK
        INTEGER departure_station_id FK
        INTEGER arrival_station_id FK
        VARCHAR route_name
    }

    Schedule {
        INTEGER schedule_id PK
        VARCHAR train_type
        INTEGER route_id FK
        TIME departure_time
        TIME arrival_time
        INTEGER price
    }

    StationRegistrationHistory {
        INTEGER history_id PK
        INTEGER user_id FK
        INTEGER route_id FK
        TIMESTAMP registered_at
        INTEGER price
    }

    User ||--o{ StationRegistrationHistory : "has"
    Route ||--o{ Schedule : "contains"
    Route ||--o{ StationRegistrationHistory : "records"
    Station ||--o{ Route : "departure"
    Station ||--o{ Route : "arrival"
