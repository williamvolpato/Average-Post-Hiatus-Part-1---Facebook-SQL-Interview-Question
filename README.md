# SQL Posts Analysis / Análise de Posts SQL

This repository contains a SQL query to analyze posts from Facebook users in 2021. The goal is to calculate the number of days between each user's first and last posts in the year, but only for users who posted at least twice during the period.

---

Este repositório contém uma consulta SQL para analisar posts de usuários do Facebook em 2021. O objetivo é calcular o número de dias entre o primeiro e o último post de cada usuário no ano, mas apenas para usuários que postaram pelo menos duas vezes durante o período.

---

## Problem Statement / Enunciado do Problema

**English**  
Given a table of Facebook posts, for each user who posted at least twice in 2021, write a query to find the number of days between each user’s first post of the year and last post of the year in the year 2021. Output the user ID and the number of days between their first and last posts.

**Português**  
Dada uma tabela de posts do Facebook, para cada usuário que postou pelo menos duas vezes em 2021, escreva uma consulta para encontrar o número de dias entre o primeiro e o último post do ano de 2021. Retorne o ID do usuário e o número de dias entre o primeiro e o último post.

---

## Table Schema / Esquema da Tabela

| Column Name   | Type      | Description                          |
|---------------|-----------|--------------------------------------|
| user_id       | integer   | Unique identifier for each user     |
| post_id       | integer   | Unique identifier for each post     |
| post_content  | text      | Content of the post                 |
| post_date     | timestamp | Date and time the post was created  |

---

## Solution / Solução

**Query:**
```sql
SELECT 
    user_id, 
    MAX(post_date::date) - MIN(post_date::date) AS days_between
FROM
    posts
WHERE
    DATE_PART('year', post_date) = 2021 
GROUP BY 
    user_id
HAVING 
    COUNT(post_id) > 1;
