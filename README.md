Baza danych postgresql
Utworzony plik docker-compose.yml powinien utworzyć kontener z bazą danych.

docker-compose up -d 

Aplikacja frontend zbuildowana do aplikacji backend

Aplikacja backend (folder o nazwie "library-main") automatycznie towrzy użytkownika admin z rolą admin (hasło: admin123)

odpalanie aplikacji przez terminal 
.\mvnw.cmd --% spring-boot:run -Dspring-boot.run.arguments="--server.port=8080"

jeśli jakim cudem nie działa plik to tu jest struktura bazy danych 

CREATE DATABASE library_db;

-- Tworzenie tabeli użytkowników
CREATE TABLE app_user (
    id bigserial PRIMARY KEY,
    username varchar(50) NOT NULL,
    password varchar(255) NOT NULL,
    role varchar(20),
    email varchar(255)
);

-- Tworzenie tabeli książek
CREATE TABLE book (
    id bigserial PRIMARY KEY,
    title varchar(255) NOT NULL,
    author varchar(255),
    isbn varchar(20),
    status varchar(20),
    year int4
);

-- Tworzenie tabeli rezerwacji z powiązaniami
CREATE TABLE reservation (
    id bigserial PRIMARY KEY,
    user_id int8 NOT NULL,
    book_id int8 NOT NULL,
    reservation_date timestamp DEFAULT CURRENT_TIMESTAMP,
    active bool DEFAULT true,
    status varchar(20),
    CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES app_user(id),
    CONSTRAINT fk_book FOREIGN KEY (book_id) REFERENCES book(id)
);


