---
title: "아마존 면접에는 SQL 코딩 질문이 10개 있어요"
description: ""
coverImage: "/assets/img/2024-05-18-10SQLCodingQuestionsinAmazonInterviews_0.png"
date: 2024-05-18 22:59
ogImage: 
  url: /assets/img/2024-05-18-10SQLCodingQuestionsinAmazonInterviews_0.png
tag: Tech
originalTitle: "10 SQL Coding Questions in Amazon Interviews"
link: "https://medium.com/@sqlfundamentals/10-sql-coding-questions-in-amazon-interviews-dcaff9277cd2"
---


Data Analyst나 Data Scientist로 취직하고 싶다면 SQL에서의 강력한 기술력이 필요합니다. 인터뷰에서는 후보자들의 문제 해결 능력과 SQL 능력을 시험하는 복잡한 SQL 코딩 문제가 종종 제시됩니다. 이 글에서는 MySQL을 사용하여 아마존의 인터뷰에서 자주 나오는 일반적인 SQL 질문들을 코드 예제와 결과와 함께 살펴보겠습니다.

![image](/assets/img/2024-05-18-10SQLCodingQuestionsinAmazonInterviews_0.png)

## 1. 두 번째로 높은 급여 찾기

직원 테이블에서 두 번째로 높은 급여를 찾는 것은 자주 나오는 질문 중 하나입니다. 서브쿼리를 사용하여 다음과 같이 수행할 수 있습니다:

<div class="content-ad"></div>

**질문:**

```sql
SELECT MAX(salary) AS SecondHighestSalary
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
```

**결과:**

```sql
| SecondHighestSalary|
|--------------------|
| 70000              |
```

이 쿼리는 결과 세트에서 최대 급여를 제외하여 두 번째로 높은 급여를 찾습니다.

<div class="content-ad"></div>

## 2. 평균 이상 급여를 받는 직원 찾기

또 다른 흔한 질문은 평균 급여보다 높은 급여를 받는 직원을 찾는 것입니다.

```js
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

결과:

<div class="content-ad"></div>

```md
이 쿼리는 각 직원의 급여를 평균 급여와 비교하여 평균 이상을 받는 사람을 찾습니다.

## 3. 직원 계층

아마존은 직원 계층을 찾는 것과 같은 계층적 데이터에 관한 질문을 할 수 있습니다. 재귀 CTE를 사용하여 직원 계층을 찾을 수 있습니다:
```

<div class="content-ad"></div>

```markdown
원들의EmployeeHierarchy

아래 결과와 같이 전체 직원 계층을 가져오는 재귀 CTE입니다.

| id | name    | manager_id |
|----|---------|------------|
| 1  | John    | NULL       |
| 2  | Alice   | 1          |
| 3  | Bob     | 1          |
| 4  | Carol   | 2          |
| 5  | Dave    | 2          |
```

<div class="content-ad"></div>

## 4. 부서별 최고 급여

각 부서별 최고 급여를 찾는 것은 또 다른 흥미로운 문제입니다:

```sql
SELECT department, MAX(salary) AS HighestSalary
FROM employees
GROUP BY department;
```

결과:

<div class="content-ad"></div>

```plaintext
```markdown
+-------------+---------------+
| department  | HighestSalary |
+-------------+---------------+
| Engineering | 90000         |
| HR          | 80000         |
| Sales       | 75000         |
+-------------+---------------+
```

이 쿼리는 부서별로 직원을 그룹화하고 각 부서의 최고 급여를 찾습니다.

## 5. 연속 결근자 식별

출석 기록에 대해 연이어 결근한 직원을 식별해야 할 수 있습니다.
```

<div class="content-ad"></div>

```markdown
WITH ConsecutiveAbsences AS (
    SELECT id, 
           date,
           LAG(date, 1) OVER (PARTITION BY id ORDER BY date) AS previous_date
    FROM attendance
    WHERE status = 'absent'
)
SELECT id, date
FROM ConsecutiveAbsences
WHERE DATEDIFF(date, previous_date) = 1;
```

Result:

```markdown
| id | date       |
|----|------------|
| 3  | 2024-05-10 |
| 3  | 2024-05-11 |
```

This query finds employees who were absent on consecutive days by comparing each absence date with the previous one.

<div class="content-ad"></div>

## 6. 러닝 토탈 계산하기

아마존 면접에는 러닝 토탈을 계산하는 질문이 포함될 수 있어요:

```sql
SELECT date, sales, 
       SUM(sales) OVER (ORDER BY date) AS running_total
FROM sales;
```

결과:

<div class="content-ad"></div>

```markdown
```sql
+------------+-------+--------------+
| 날짜       | 매출  | 누적합계      |
+------------+-------+--------------+
| 2024-05-01 | 100   | 100          |
| 2024-05-02 | 200   | 300          |
| 2024-05-03 | 150   | 450          |
+------------+-------+--------------+
```

이 쿼리는 시간에 따른 매출의 누적 합계를 계산합니다.

## 7. 구매를 한 번도 하지 않은 고객

구매를 한 번도 하지 않은 고객을 찾기 위해 LEFT JOIN을 사용할 수 있습니다:
```

<div class="content-ad"></div>

바로 보라 카드모래 예술로나와 함께합니다! ✨

```sql
SELECT c.id, c.name
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
WHERE o.id IS NULL;
```

결과:

```sql
+----+--------+
| id | name   |
+----+--------+
| 4  | Dave   |
+----+--------+
```

이 쿼리는 주문 내역이 하나도 없는 고객을 찾아냅니다. 🌟

<div class="content-ad"></div>

## 8. 중복 레코드 식별

당신에게 테이블에서 중복 레코드를 식별하라는 요청을 받을 수 있습니다:

```sql
SELECT name, email, COUNT(*)
FROM users
GROUP BY name, email
HAVING COUNT(*) > 1;
```

결과:

<div class="content-ad"></div>

이 쿼리는 중복된 이름과 이메일 조합을 가진 사용자를 식별합니다.

## 9. 카테고리별 상위 N개 레코드

카테고리별 상위 N개 레코드를 찾는 것은 일반적인 고급 SQL 질문입니다:

<div class="content-ad"></div>

```sql
WITH RankedSales AS (
    SELECT product, category, sales,
           ROW_NUMBER() OVER (PARTITION BY category ORDER BY sales DESC) AS rank
    FROM sales
)
SELECT product, category, sales
FROM RankedSales
WHERE rank <= 3;
```

Result:

```sql
| product | category    | sales |
|---------|-------------|-------|
| A       | Electronics | 1000  |
| B       | Electronics | 800   |
| C       | Electronics | 600   |
| D       | Furniture   | 900   |
| E       | Furniture   | 850   |
| F       | Furniture   | 800   |
```

This query finds the top 3 products in each category based on sales.

<div class="content-ad"></div>

## 10. 월간 성장률

월간 성장률을 계산하려면 윈도우 함수를 사용해야 합니다:

```js
SELECT month, sales,
       sales - LAG(sales, 1) OVER (ORDER BY month) AS growth
FROM monthly_sales;
```

결과:

<div class="content-ad"></div>

```markdown
+-------+-------+--------+
|  월   |  매출 |  성장률 |
+-------+-------+--------+
|  1월  | 1000  |   NULL  |
|  2월  | 1100  |  100    |
|  3월  | 1200  |  100    |
+-------+-------+--------+
```

이 쿼리는 매출의 월간 성장률을 계산합니다.

## 결론

아마존 면접 준비에는 고급 SQL 개념을 이해하고 복잡한 비즈니스 문제를 해결할 수 있는 능력이 필요합니다. 이러한 SQL 코딩 문제를 숙달하고 실제 데이터로 연습함으로써, 면접관들을 감명시키고 아마존에서 꿈에 그리던 직장을 확보할 수 있을 것입니다.
```

<div class="content-ad"></div>

# SQL 기초

당신의 시간과 관심에 감사드립니다! 🚀
더 많은 콘텐츠는 SQL 기초에서 찾아볼 수 있어요! 💫