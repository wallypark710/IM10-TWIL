## Datatypes in SQLite Version 3

SQLite 는 다른 관계형 데이터베이스들과 달리 **동적 자료형**을 지원한다.

이를 위해 2가지 Storage Class 와 Type Affinity 라는 두가지 개념을 도입한다.

<br/>

### Storage Class

데이터베이스에 저장되는 value 가 어떤 타입으로 저장이 되었는지 표시하는 메타데이터 정도라고 생각하면 된다.

특이한 점은 column 에 적용되지 않고 각각 모든 value 에 적용된다.

*Storage class 는 아래와 같이 총 5개가 있다.*

**1. NULL**

- The value is a NULL value.

**2. INTEGER**	

- The value is a signed integer, stored in 1, 2, 3, 4, 6, or 8 bytes depending on the magnitude of the value.

**3. REAL**

- The value is a floating point value, stored as an 8-byte IEEE floating point number.

**4. TEXT**

-The value is a text string, stored using the database encoding (UTF-8, UTF-16BE or UTF-16LE).

**5. BLOB**

- The value is a blob of data, stored exactly as it was input.

---

- **Boolean Type** 의 경우 `INTEGER` 로 0 혹은 1 로 저장된다.
- **Datetime** 의 경우 `INTEGER` 로 UNIX 시간을 넣거나, `TEXT` 로 `"YYYY-MM-DD HH:MM:SS.SSS"` 형태로 저장한다.

<br/>

### Type Affinity

SQLite 는 schema 를 정의할 때 타입을 정의하는게 아니라, 저장되는 데이터에 어떤 type affinity 가 적용될 지 정의하는 것이다.

Type affinity 가 적용되면 데이터가 저장되기 전 input 데이터를 확인하여 알맞는 storage class 를 결정한다.

즉, schema 에 `INTEGER` 라고 정의해도 반드시 `INTEGER` 로 저장되지 않을 수도 있다.

<br/>

*아래는 schema 정의 시 해당 column 에 적용되는 type affinity 목록이다.*

**1. INTEGER**

- If the declared type contains the string "INT" then it is assigned INTEGER affinity.

**2. TEXT**

- If the declared type of the column contains any of the strings "CHAR", "CLOB", or "TEXT" then that column has TEXT affinity. Notice that the type VARCHAR contains the string "CHAR" and is thus assigned TEXT affinity.

**3. BLOB**

- If the declared type for a column contains the string "BLOB" or if no type is specified then the column has affinity BLOB.

**4. REAL**

- If the declared type for a column contains any of the strings "REAL", "FLOA", or "DOUB" then the column has REAL affinity.

**5. NUMERIC**

- Otherwise, the affinity is NUMERIC.

<br/>

*아래는 type affinity 별 데이터가 입력되었을 때 어떤 storage class 로 저장할 지 결정하는 기준이다.*

**1. TEXT**

- A column with TEXT affinity stores all data using storage classes NULL, TEXT or BLOB. If numerical data is inserted into a column with TEXT affinity it is converted into text form before being stored.

**2. NUMERIC**

- A column with NUMERIC affinity may contain values using all five storage classes. When text data is inserted into a NUMERIC column, the storage class of the text is converted to INTEGER or REAL (in order of preference) if such conversion is lossless and reversible. For conversions between TEXT and REAL storage classes, SQLite considers the conversion to be lossless and reversible if the first 15 significant decimal digits of the number are preserved. If the lossless conversion of TEXT to INTEGER or REAL is not possible then the value is stored using the TEXT storage class. No attempt is made to convert NULL or BLOB values.

- A string might look like a floating-point literal with a decimal point and/or exponent notation but as long as the value can be expressed as an integer, the NUMERIC affinity will convert it into an integer. Hence, the string '3.0e+5' is stored in a column with NUMERIC affinity as the integer 300000, not as the floating point value 300000.0.

**3. INTEGER**

- A column that uses INTEGER affinity behaves the same as a column with NUMERIC affinity. The difference between INTEGER and NUMERIC affinity is only evident in a [CAST expression](https://www.sqlite.org/lang_expr.html#castexpr).

**4. REAL**

- A column with REAL affinity behaves like a column with NUMERIC affinity except that it forces integer values into floating point representation. (As an internal optimization, small floating point values with no fractional component and stored in columns with REAL affinity are written to disk as integers in order to take up less space and are automatically converted back into floating point as the value is read out. This optimization is completely invisible at the SQL level and can only be detected by examining the raw bits of the database file.)

**5. BLOB**

- A column with affinity BLOB does not prefer one storage class over another and no attempt is made to coerce data from one storage class into another.

<br/>

## **References**

[Datatypes In SQLite Version 3](https://www.sqlite.org/datatype3.html)

[[SQLite] 동적 자료형 (Dynamic Datatype)](https://thinking-jmini.tistory.com/24)